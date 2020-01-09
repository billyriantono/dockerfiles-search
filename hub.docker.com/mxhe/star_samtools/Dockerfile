FROM quay.io/biocontainers/samtools:1.9--h8571acd_11

# replace BusyBox with newer version for xargs -P support
ADD https://busybox.net/downloads/binaries/1.28.1-defconfig-multiarch/busybox-x86_64 /usr/local/busybox
RUN chmod ugo+rx /usr/local/busybox && mv /usr/local/busybox /bin

# add STAR from STAR biocontainer
COPY --from=quay.io/biocontainers/star:2.7.2b--0 /usr/local/bin/STAR /usr/local/bin/STAR
