# Kubernetes admin nix shell

We want to implement reusable kubernetes admin shell using nix-shell 
that can be quickly deployed to any server or inside container,
without any needed dependencies.

## Tools

These are the tools we are going to use:

- [nix](https://nixos.org/nix/)
- [home-manager](https://github.com/rycee/home-manager)
- [nix-bundle](https://github.com/matthewbauer/nix-bundle)

## Methods of injection

First we need to push admin shell image to docker registry. A pod is deployed
on a server running target pod/container. Based on desired access different
method is used.

### Accessing server

Execute privileged pod on the target server with shared network and
process namespace. Mount host root inside container under `/mnt`.

### Accessing pod

1. Method: pod container injection

Modify existing deployment/statefuset/daemonset and add additional privileged
or unprivileged container that enables process namespace sharing.

2. Method: nsenter

Deploy privileged pod on a server where target pod is running with process
namespace shared with host. Identify target pod container and nsenter into
process/network namespace of target container.
