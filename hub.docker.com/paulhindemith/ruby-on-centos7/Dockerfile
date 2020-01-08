ARG RUBY_PATH=/usr/local
ARG RUBY_VERSION=2.6.5

FROM centos:7 AS rubybuild

ARG RUBY_PATH

ARG RUBY_VERSION

RUN yum install -y \
    epel-release \
    openssl-devel \
    readline-devel\
    zlib-devel \
    wget \
    curl \
    git \
    dtach \
    hash-slinger \
    bzip2 \
    tar \
    libffi-devel \
    libxslt-devel \
&&  yum groupinstall "Development Tools" -y \
&&  yum clean all

ARG RUBY_PATH
ARG RUBY_VERSION

RUN git clone git://github.com/rbenv/ruby-build.git $RUBY_PATH/plugins/ruby-build \
&&  $RUBY_PATH/plugins/ruby-build/install.sh

RUN ruby-build $RUBY_VERSION $RUBY_PATH/

FROM centos:7

ARG RUBY_PATH

ENV PATH $RUBY_PATH/bin:$PATH

COPY --from=rubybuild $RUBY_PATH $RUBY_PATH

# exec form, not shell form.
CMD ["irb"]
