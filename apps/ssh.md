# SSH

## SSH-over-SSH tunnel

You can initiate ssh-over-ssh tunnel using `ProxyJump` option.

```bash
$ ssh -o ProxyJump='root@proxy.server.net'
```

Putting into `~/.ssh/config`:

```
Host *.local.net
ProxyJump root@192.168.122.1
```
