# Qemu App notes

## Usefull commands

### Convert encrypted luks image to qcow2

```
qemu-img convert --image-opts --object secret,id=sec0,file=pass.b64,format=base64 -O qcow2 driver=luks,file.driver=file,file.filename=projects.luks,key-secret=sec0 projects.qcow2
```
### Mount qemu image

```bash
sudo modprobe nbd max_part=8
sudo qemu-nbd --object secret,id=sec0,file=pass.b64,format=base64 --image-opts --connect=/dev/nbd0 driver=luks,file.driver=file,file.filename=firstorbital.luks,key-secret=sec
```

### Live partition resize

```bash
qemu-img resize <name>.qcow2 +20G
```

Notify qemu about block resize

```bash
virsh qemu-monitor-command <name> info block --hmp # get disk info
virsh qemu-monitor-command <name> block_resize drive-virtio-disk0 60G --hmp # resize to a new size
```

Now run fdisk in vm, remove old partition, create new bigger one, and run resize2fs.
