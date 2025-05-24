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

        .merkle-damgard input,
        .merkle-damgard button {
            margin: 5px 0;
            padding: 8px;
        }

        .result {
            margin-top: 15px;
            font-weight: bold;
        }
        .iteration {
            margin-top: 15px;
            font-weight: bold;
            white-space: pre-wrap;
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

        <button type="button" onclick="calculate()">Calc</button>
    </form>

    <div class="result" id="paddingResultField">After Padding: </div>
    <div class="iteration" id="iteration">Iteration: </div>
    <div class="result" id="result">Result: </div>

    <script>
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