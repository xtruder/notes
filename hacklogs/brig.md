# Testing brig on NixOS (2019-03-02)

I decided to try out brig a file synchronization on top of ipfs with git like interface and FUSE filesystem 

## 1. Creating nixos package

As package for nixos does not exist yet, we need to package it first.
It's a go package with vendor folder, so this should not be too hard.
