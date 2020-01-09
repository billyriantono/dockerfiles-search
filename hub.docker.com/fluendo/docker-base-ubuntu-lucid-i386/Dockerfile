FROM scratch
ADD rootfs.tar.xz /

# Fix the uname call outputing 64 bits arch on 32 bits docker image.
ENTRYPOINT ["/usr/bin/linux32", "--"]

CMD ["/bin/bash"]
