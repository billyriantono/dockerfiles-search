FROM keithseahus/base-ubuntu-14.04lts
MAINTAINER Keisuke Takahashi <keithseahus@gmail.com>

ENV REFRESHED_AT 2014-12-11

USER root

RUN apt-get update
RUN apt-get upgrade -y

ENV ERLANG_VERSION 17.4

RUN locale-gen en_US.UTF-8
ENV LANG en_US.UTF-8
ENV LANGUAGE en_US:en
ENV LC_ALL en_US.UTF-8

RUN apt-get install -y \
    libncurses5-dev \
    openssl \
    libssl-dev \
    fop \
    xsltproc \
    openjdk-6-jdk \
    unixodbc-dev \
    g++ \
    libwxbase2.8 \
    libwxgtk2.8-dev \
    libqt4-opengl-dev \
    libgtk2.0-dev \
    systemtap-sdt-dev \
    libxml2-utils

ENV PATH /bin:/sbin:/usr/bin:/usr/sbin:/usr/local/bin:/usr/local/sbin:/usr/local/erlang/bin

ADD http://erlang.org/download/otp_src_${ERLANG_VERSION}.tar.gz /usr/local/src/
RUN cd /usr/local/src \
    && tar xf otp_src_${ERLANG_VERSION}.tar.gz \
    && cd otp_src_${ERLANG_VERSION} \
    && ./configure --prefix=/usr/local/erlang-otp-${ERLANG_VERSION} --enable-threads --enable-dirty-schedulers --enable-smp-support --enable-kernel-poll --enable-sctp --enable-vm-probes --enable-m64-build --with-termcap --with-dynamic-trace=dtrace --with-ssl \
    && make \
    && make install \
    && ln -snf /usr/local/erlang-otp-${ERLANG_VERSION} /usr/local/erlang \
    && echo -n '/usr/local/erlang/lib' | tee /etc/ld.so.conf.d/erlang

EXPOSE 4369 80 443 8080

USER dev
ENV PATH /bin:/sbin:/usr/bin:/usr/sbin:/usr/local/bin:/usr/local/sbin:/usr/local/erlang/bin

