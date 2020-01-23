FROM scratch
MAINTAINER don.raikes@oracle.com
ADD oraclelinux-7.2-rootfs.tar.xz /

## 02/09/2017 draikes - added yum upgrade
RUN	yum upgrade -y

# overwrite this with 'CMD []' in a dependent Dockerfile
CMD ["/bin/bash"]
