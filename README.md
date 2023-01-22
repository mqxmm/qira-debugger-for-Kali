# Install QIRA (QEMU Interactive Runtime Analyser)
original: https://github.com/geohot/qira

## Running:
```bash
qira -s file.bin
```

## Install:
### step 1:
Clone this repository.

```bash
https://github.com/mqxmm/qira-debugger-for-Kali.git
```

### step 2:

Unpacking 

```bash
apt -y install docker.io zstd
cd / ; pzstd -d < root_Desktop_qira.tar.zst | tar x
```

### step 3:

Installing

```bash
pzstd -d < qira-img.tar.zst | docker load
```

### step 4:

Create container

```bash
docker run -d -v /mnt:/mnt -v /root:/root --privileged --network host --pid host --restart always --name qira qira-img sleep infinity
```

### step 5:

Create wrapper

```bash
# cat /usr/local/bin/qira 
#!/bin/bash
INTERACT=-i
if [ -t 0 ] ; then INTERACT=-ti ; fi
exec docker exec $INTERACT -w "`pwd`" qira qira "$@"
```
