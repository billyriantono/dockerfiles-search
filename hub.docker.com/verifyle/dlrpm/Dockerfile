FROM centos:latest

ARG BUILD_DATE

LABEL maintainer="docker@aquaron.com" \
 org.label-schema.build-date=$BUILD_DATE \
 org.label-schema.docker.cmd="docker run --rm -t -v $PWD:/data verifyle/dlrpm" \
 org.label-schema.description="Download RPM" \
 org.label-schema.name="dlrpm" \
 org.label-schema.vcs-url="https://github.com/verifyle/dlrpm" \
 org.label-schema.vendor="verifyle" \
 org.label-schema.version="1.1"

COPY files/runme.sh /usr/local/bin

RUN yum -y update && yum clean all

ENTRYPOINT [ "/usr/local/bin/runme.sh" ]

CMD [ "-process" ]
