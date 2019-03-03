# Libvirt App notes

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

### Change disk IOPS

```
virsh blkdeviotune <name> vda --total-iops-sec 1000
```

### Listing disks attached to domain

To list disks attached to domain run:

```
virsh --connect qemu:///system domblklist <domain_name>
```

### Flattening images

If disk was created from base image, you can flatten it using this command:

```
virsh --connect qemu:///system blockpull <domain_name> <disk> --wait
```

### Live migration of vms

To do live migration you need to make sure migration ports in the range 49152-49215 are opened,
this can be done in nixos using:

```
networking.firewall.allowedTCPPortRanges = [{ from = 49152; to = 49215; }];
```

You will also need to copy any backing images (like nixos base image) to same locations on other host
and define same storage pools.
