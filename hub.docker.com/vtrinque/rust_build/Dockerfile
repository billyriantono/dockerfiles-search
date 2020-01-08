FROM vtrinque/base

MAINTAINER Valentin Trinque <val.trinque@gmail.com>

# install dependencies
USER root
RUN yum clean all && yum update -y && yum install -y \
    curl \
    tar \

# can be overriden by setting up a new USER clause or -u option
USER app

# directory for all rust-related stuff
RUN mkdir -p /home/app/env/rust

# install rust compiler and cargo
RUN curl -s https://static.rust-lang.org/rustup.sh > /home/app/env/rust/install.sh
RUN chmod +x /home/app/env/rust/install.sh
RUN sh /home/app/env/rust/install.sh --disable-sudo -y

# define env variables needed by rust
ENV LD_LIBRARY_PATH=/usr/local/lib/

# useful aliases
RUN echo 'alias rustup="sh /home/app/env/rust/install.sh --disable-sudo"' >> /home/app/.bashrc
