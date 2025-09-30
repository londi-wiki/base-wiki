---
weight: 999
title: "Cloud Image"
description: ""
icon: "article"
date: "2025-09-30T09:27:00+02:00"
lastmod: "2025-09-30T09:27:00+02:00"
draft: true
toc: true
katex: false
---

## Simple cloud image

```bash
wget https://cloud-images.ubuntu.com/noble/current/noble-server-cloudimg-amd64.img
qm create 8000 --memory 2048 --name ubuntu-cloud --net0 virtio,bridge=vmbr0
qm set 8000 --cores 2 --cpu host
qm set 8000 --bios ovmf --machine q35 --efidisk0 vms:0,pre-enrolled-keys=1
qm importdisk 8000 noble-server-cloudimg-amd64.img vms
qm set 8000 --scsihw virtio-scsi-pci --scsi0 vms:vm-8000-disk-0
qm set 8000 --ide2 vms:cloudinit
qm set 8000 --boot c --bootdisk scsi0
qm set 8000 --serial0 socket --vga serial0
qm resize 8000 scsi0 +10G
qm set 8000 --agent enabled=1

qm set 8000 --ipconfig0 ip=dhcp
# qm set 8000 --sshkey ~/.ssh/id_rsa.pub
qm set 8000 --ciuser ubuntu
qm set 8000 --nameserver 10.10.0.1 --searchdomain lan


qm template 8000
```

After that, create a template from it.

