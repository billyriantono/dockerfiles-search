FROM gliderlabs/alpine:3.3
MAINTAINER Joseph Yølk Chiocchi <joe@yolk.cc>

WORKDIR /root
VOLUME /root/.aws

ENTRYPOINT ["/usr/bin/aws"]
CMD ["help"]

RUN apk-install less=481-r2 groff=1.22.3-r1 py-pip=7.1.2-r0 bash
RUN pip install --upgrade pip
RUN pip install awscli==1.10.39
