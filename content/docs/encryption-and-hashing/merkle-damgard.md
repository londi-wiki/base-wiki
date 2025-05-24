---
weight: 999
title: "Merkle Damgard Verfahren"
description: ""
icon: "article"
date: "2025-05-24T22:56:37+02:00"
lastmod: "2025-05-24T22:56:37+02:00"
draft: false
toc: true
---

# Merkle Damgård Verfahren

{{< rawhtml >}}

<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <title>Simple Calculator</title>
    <style>
        .merkle-damgard {
            font-family: Arial, sans-serif;
            padding: 20px;
            color: var(--doc-nav-title-link-color);
            background-color: #181921;
        }

        .merkle-damgard input {
            margin: 8px 0 16px 0;
            padding: 10px;
            width: 100%;
            max-width: 300px;
            border-radius: 6px;
            border: 1px solid #3e4154;
            background-color: #242632;
            color: #e1e2e6;
            font-size: 14px;
            transition: all 0.3s ease;
            box-sizing: border-box;
        }

        .merkle-damgard input:focus {
            border-color: var(--doc-nav-title-link-color);
            outline: none;
            box-shadow: 0 0 0 2px rgba(86, 113, 245, 0.2);
        }

        .merkle-damgard label {
            font-size: 14px;
            font-weight: 500;
            color: #e1e2e6;
            margin-bottom: 4px;
            display: block;
        }

        .merkle-damgard button {
            margin-top: 16px;
            padding: 10px 20px;
            color: white;
            border: none;
            border-radius: 6px;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.2s ease;
            font-size: 14px;
        }

        .merkle-damgard button.primary {
            background-color:rgb(100, 125, 252);
        }

        .merkle-damgard button.secondary {
            background-color:rgb(15, 196, 150);
        }

        .merkle-damgard button:hover {
            transform: translateY(-1px);
        }

        .merkle-damgard button.primary:hover {
            background-color: #4a61d8;
        }

        .merkle-damgard button.secondary:hover {
            background-color: rgb(13, 167, 128);
        }

        .merkle-damgard button:active {
            transform: translateY(1px);
        }

        .result {
            margin-top: 20px;
            font-weight: bold;
            background-color: #242632;
            padding: 12px;
            border-radius: 6px;
            border-left: 3px solid #5671f5;
        }
        
        .iteration {
            margin-top: 20px;
            font-weight: bold;
            white-space: pre-wrap;
            background-color: #242632;
            padding: 12px;
            border-radius: 6px;
            border-left: 3px solid #5671f5;
        }
    </style>
</head>

<body class="merkle-damgard">
    <h2>Merkle Damgård Verfahren</h2>
    <form id="calcForm">
        <label for="val1">'b' value:</label><br>
        <input type="number" id="val1" name="val1" value="2"><br>

        <label for="val2">'r' value:</label><br>
        <input type="number" id="val2" name="val2" value="4"><br>

        <label for="val3">Input 'x' (binary):</label><br>
        <input type="number" id="val3" name="val3" value="01010"><br>

        <label for="val4">Init value 'u':</label><br>
        <input type="number" id="val4" name="val4" value="10"><br>

        <button type="button" id="clear-button" class="secondary" onclick="clearForm()">Clear</button>
        <button type="button" id="calc-button" class="primary" onclick="calculate()">Calc</button>
    </form>

    <div class="result" id="paddingResultField">After Padding: </div>
    <div class="iteration" id="iteration">Iteration: </div>
    <div class="result" id="result">Result: </div>

    <script>
        function clearForm() {
            console.log('clear');
            document.getElementById('val1').value = '2';
            document.getElementById('val2').value = '4';
            document.getElementById('val3').value = '01010';
            document.getElementById('val4').value = '10';

            document.getElementById('paddingResultField').textContent = 'After Padding: ';
            document.getElementById('iteration').textContent = 'Iteration: ';
            document.getElementById('result').textContent = 'Result: ';
        }

        function calculate() {
            const b = parseInt(document.getElementById('val1').value) || 0;
            const r = parseInt(document.getElementById('val2').value) || 0;
            const input = document.getElementById('val3').value;
            const u = document.getElementById('val4').value;
            
            // Padding Verfahren
            const inputLength = input.length;
            console.log(`Input length: ${inputLength}`);
            let inputWithPadding = input + '1';
            const zeroPadding = (inputWithPadding.length + r) % b;
            let r_binary = inputLength.toString(2);
            while (r_binary.length < r) {
                r_binary = '0' + r_binary;
            }
            console.log(`r_binary: ${r_binary}`);
            console.log(`Zero padding needed: ${zeroPadding}`);
            const inputAfterPadding = `${input} 1${zeroPadding > 0 ? zeroPadding * '0' : ''} ${r_binary}`
            console.log(`tf expected: 01010 1 0101`);
            console.log(`tf: ${inputAfterPadding}`);

            document.getElementById('paddingResultField').textContent = 'After Padding: ' + inputAfterPadding;

            // Iterationsverfahren
            const inputAfterPadding_trimmed = inputAfterPadding.replace(/\s/g, '');
            const binaryBlocks = [];
            let i = 0;
            while (i < inputAfterPadding_trimmed.length) {
                binaryBlocks.push(inputAfterPadding_trimmed.slice(i, i + b));
                i = i+b;
            }
            console.log(`Binary blocks: ${binaryBlocks}`);

            
            let iterationText = 'Iteration: ';
            let startBlock = u;
            for(let i = 0; i < binaryBlocks.length; i++) {
                console.log(`Start value: ${startBlock}`);
                iterationText += `\nIteration ${i + 1}: ${startBlock} with block ${binaryBlocks[i]}`;

                const binaryBlock = binaryBlocks[i];
                const firstValue = startBlock.charAt(0) ^ startBlock.charAt(1)
                console.log(`${startBlock.charAt(0)} xor ${startBlock.charAt(1)}: ${firstValue}`);
                iterationText += `\n${startBlock.charAt(0)} xor ${startBlock.charAt(1)}: ${firstValue}`;

                const secondValue = binaryBlock.charAt(0) ^ binaryBlock.charAt(1)
                console.log(`${binaryBlock.charAt(0)} xor ${binaryBlock.charAt(1)}: ${secondValue}`);
                iterationText += `\n${binaryBlock.charAt(0)} xor ${binaryBlock.charAt(1)}: ${secondValue}`;

                startBlock = `${firstValue}${secondValue}`;
                console.log('---');
                iterationText += `\nConcatenated value: ${startBlock}\n---`;
            }
            console.log(`Final value: ${startBlock}`);
            iterationText += `\nFinal value: ${startBlock}`;

            document.getElementById('iteration').textContent = iterationText;
            document.getElementById('result').textContent = 'Result: ' + startBlock;
        }
    </script>
</body>

</html>

{{< /rawhtml >}}