FROM centos:latest
MAINTAINER William Fleming <wfleming@grumpysysadm.com>

RUN yum install -y epel-release 

RUN yum install -y rpm-build ruby rubygems git wget curl file make automake autoconf curl-devel zlib-devel ruby-devel binutils gcc-c++ gcc python zip rhash openssl-devel build-essential pkg-config libudev-devel

RUN curl -sSf https://static.rust-lang.org/rustup.sh -o rustup.sh && sh rustup.sh --disable-sudo --yes --channel=nightly

ENV RUST_BACKTRACE 1
