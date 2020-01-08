FROM rust:1.36.0 AS cross-compiler

RUN rustup target add x86_64-unknown-linux-musl && \
wget 'https://toolchains.bootlin.com/downloads/releases/toolchains/x86-64-core-i7/tarballs/x86-64-core-i7--musl--bleeding-edge-2018.11-1.tar.bz2' && \
mkdir -p /opt/toolchains && \
tar jxf x86-64-core-i7--musl--bleeding-edge-2018.11-1.tar.bz2 -C /opt/toolchains/ && \
rm -f x86-64-core-i7--musl--bleeding-edge-2018.11-1.tar.bz2 && \
mv /opt/toolchains/x86-64-core-i7--musl--bleeding-edge-2018.11-1 /opt/toolchains/x86-64_musl && \
mkdir ~/.cargo && \
echo '[target.x86_64-unknown-linux-musl]' > ~/.cargo/config && \
echo 'linker = "x86_64-buildroot-linux-musl-gcc"' >> ~/.cargo/config && \
echo 'rustflags = [' >> ~/.cargo/config && \
echo '    "-C", "link-arg=-lgcc",' >>  ~/.cargo/config && \
echo '    "-C", "target-feature=+crt-static"' >>  ~/.cargo/config && \
echo ']' >>  ~/.cargo/config

ENV PATH $PATH:/opt/toolchains/x86-64_musl/bin