FROM pushamp/manylinux-openssl-x86_64
COPY build_rust /build_rust
RUN build_rust/build_rust.sh
ENV PATH=/root/rust/bin:/opt/rh/devtoolset-2/root/usr/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
ENV LD_LIBRARY_PATH=/opt/rh/devtoolset-2/root/usr/lib64:/opt/rh/devtoolset-2/root/usr/lib:/usr/local/lib64:/usr/local/lib:/root/rust/lib
