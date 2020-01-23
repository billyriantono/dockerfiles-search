FROM multiarch/alpine:aarch64-edge

RUN apk update
RUN apk add alpine-sdk build-base apk-tools alpine-conf busybox fakeroot xorriso squashfs-tools mtools dosfstools grub-efi parted e2fsprogs multipath-tools
RUN adduser -D -g "" -G abuild build
RUN echo "build ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers
RUN sudo -H -u build /bin/sh -c 'source /etc/profile; abuild-keygen -i -a && ls -l /etc/apk/keys'
