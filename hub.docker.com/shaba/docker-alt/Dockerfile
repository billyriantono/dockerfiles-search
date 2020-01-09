FROM scratch

MAINTAINER \
[Alexey Shabalin <shaba@altlinux.org] \
[Gleb Fotengauer-Malinovskiy <glebfm@altlinux.org>]

ADD alt-sisyphus-x86_64-20180515.tar.xz /


# make systemd-detect-virt return "docker"
# See: https://github.com/systemd/systemd/blob/aa0c34279ee40bce2f9681b496922dedbadfca19/src/basic/virt.c#L434
RUN mkdir -p /run/systemd && echo 'docker' > /run/systemd/container

# overwrite this with 'CMD []' in a dependent Dockerfile
CMD ["/bin/bash"]
