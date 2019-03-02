# Testing brig on NixOS (2019-03-02)

I decided to try out brig a file synchronization on top of ipfs with git like interface and FUSE filesystem 

## 1. Creating nixos package

As package for nixos does not exist yet, we need to package it first.
It's a go package with vendor folder, so this should not be hard, since
we can directly use `buildGoPackage`.

For some reason building takes a long time, but produces working brig binary.

## 2. Testing brig

- Initialized brig on machine 1 using:

```
brig --repo ~/.brig init offline@x-truder.net/desktop
```

- Initialized brig on machine 2 using:

```
brig --repo ~/.brig init offline@x-truder.net/offline
```

- Mounted brig fs and copied nixos iso to it

```
mkdir ~/data
brig mount ~/data
cp nixos.iso ~/data/nixos.iso
```

- Adding brig remotes

```
brig whoami -> displays node fingerprint
brig remote add <name_of_remote> <fingerprint>
```

- Sync

You need to explicity sync things, there does not seem to be auto sync, but you can handle that with something like cronjob

```
brig sync <name_of_remote>
```
