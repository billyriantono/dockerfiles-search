FROM amazonlinux:2017.03
MAINTAINER Juan Carlos Pazos Mandiá <jucapaman@gmail.com>

RUN yum groupinstall "Development Tools" -y && \
    yum install wget ncurses-devel openssl-devel -y && \
    wget http://erlang.org/download/otp_src_20.0.tar.gz && \
    tar -zxvf otp_src_20.0.tar.gz && \
    rm otp_src_20.0.tar.gz && \
    cd otp_src_20.0/ && \
    ./configure && \
    make && \
    make install && \
    cd .. && \
    rm -rf otp_src_20.0/ && \
    wget https://github.com/elixir-lang/elixir/archive/v1.4.5.zip && \
    unzip v1.4.5.zip && \
    rm v1.4.5.zip && \
    cd elixir-1.4.5/ && \
    make && \
    make install && \
    cd .. && \
    rm -rf elixir-1.4.5/
