FROM ubuntu:trusty

MAINTAINER statianzo

ENV PATH /app/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
ENV PORT 5000
ENV DEBIAN_FRONTEND noninteractive
EXPOSE 5000

RUN echo "force-unsafe-io" > /etc/dpkg/dpkg.cfg.d/02apt-speedup
RUN echo "exit 101" > /usr/sbin/policy-rc.d
RUN echo 'DPkg::Post-Invoke {"/bin/rm -f /var/cache/apt/archives/*.deb || true";};' > /etc/apt/apt.conf.d/no-cache


RUN LC_ALL=C \
    apt-get update && \
    apt-get install     -y   \
    sudo                     \
    git                      \
    supervisor               \
    curl                     \
    libpcre3                     \
    libpcre3-dev                     \
    libssl-dev                     \
    lua5.1 \
    luarocks                     \
    stunnel4                     \
    build-essential        && \
    apt-get clean && \
    rm -rf /var/cache/apt/* /var/lib/apt/lists/*

# Make node available as "node"
RUN ln -s /usr/bin/nodejs /usr/local/bin/node

RUN locale-gen en_US.UTF-8
ENV LANG en_US.UTF-8

RUN useradd --no-create-home builder && \
    chgrp -R builder /usr/local && \
    find /usr/local -type d | xargs chmod g+w && \
    echo "builder ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers.d/builder && \
    chmod 0440 /etc/sudoers.d/builder

RUN useradd --no-create-home app

ADD /bin/proc2super /usr/local/bin/

USER builder

RUN curl -L -o /tmp/ngx_openresty.tar.gz http://openresty.org/download/ngx_openresty-1.5.11.1.tar.gz

RUN cd /tmp && \
    tar xzf ngx_openresty.tar.gz  && \
    cd ngx_* && \
    ./configure --prefix=/usr && \
    make && \
    sudo make install &&\
    cd / && rm -rf /tmp/ngx*

RUN sudo ln -s /usr/nginx/sbin/nginx /usr/bin/openresty
