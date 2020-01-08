FROM fedora:latest

ENV RUSTUP_HOME=/rustup CARGO_HOME=/cargo PATH="/cargo/bin:${PATH}"
RUN dnf upgrade -y --refresh
RUN dnf install -y @development-tools
RUN dnf install -y mingw64-gcc mingw64-gtk3 mingw64-winpthreads-static mingw64-pkg-config zip findutils gcc-c++ glib2-devel gtk3-devel systemd-devel msitools
RUN dnf clean all -y
RUN curl https://sh.rustup.rs -sSf | sh -s -- -y
RUN rustup target add x86_64-pc-windows-gnu
RUN rustup install nightly
RUN rustup update
