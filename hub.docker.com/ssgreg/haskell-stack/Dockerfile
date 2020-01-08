FROM centos:latest

ADD build.sh /build.sh
ADD entrypoint.sh /entrypoint.sh

RUN \
    curl -sSL https://download.fpcomplete.com/centos/7/fpco.repo | tee /etc/yum.repos.d/fpco.repo && \
    yum -y install stack zlib-devel && \
    yum -y group install "Development Tools" && \
    cd /tmp && \
    stack new test --resolver lts-7.12 && \
    cd /tmp/test && \
    stack setup && \
    cd && \
    rm -rf /tmp/test

CMD ["/entrypoint.sh"]

