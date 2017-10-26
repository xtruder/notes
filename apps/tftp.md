# TFTP

## Running tftpd

```
sudo atftpd --trace -v --daemon --no-fork --user root --port 69 --logfile - $PWD
```
