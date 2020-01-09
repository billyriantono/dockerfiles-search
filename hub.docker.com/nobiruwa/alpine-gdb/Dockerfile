# Alpine for compiling something
FROM alpine

ARG gdb=gdb-8.3

# install development toolkit.
RUN apk add --update alpine-sdk nasm linux-headers texinfo gdb bash strace
RUN curl https://ftp.gnu.org/gnu/gdb/${gdb}.tar.gz -o /tmp/${gdb}.tar.gz && \
    cd /tmp && \
    tar zxf ${gdb}.tar.gz && \
    cd ${gdb} && \
    ./configure --prefix=/opt/${gdb} && \
    make && \
    make install

ENV PATH="/opt/${gdb}/bin:${PATH}"
