# Qemu App notes

## Usefull commands

### Convert encrypted luks image to qcow2

```
qemu-img convert --image-opts --object secret,id=sec0,file=pass.b64,format=base64 -O qcow2 driver=luks,file.driver=file,file.filename=projects.luks,key-secret=sec0 projects.qcow2
```
### Mount qemu image

```bash
sudo qemu-nbd --object secret,id=sec0,file=pass.b64,format=base64 --image-opts --connect=/dev/nbd0 driver=luks,file.driver=file,file.filename=firstorbital.luks,key-secret=sec
sudo modprobe nbd max_part=8
```
