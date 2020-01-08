FROM dqneo/perlimagemagick

MAINTAINER DQNEO

# nano: for debug
# expat-devel: for XML::Simple
# openssl, openssl-devel: for LWP::Protocol::https
RUN yum install -y nano expat-devel openssl openssl-devel; yum clean all

RUN mkdir -p /opt/app

WORKDIR /opt/app

COPY cpanfile /opt/app/cpanfile
COPY cpanfile.snapshot /opt/app/cpanfile.snapshot

RUN carton install --deployment \
    && rm -rf /opt/app/local/cache

CMD ["perldoc -l LWP::Protocol::https"]
