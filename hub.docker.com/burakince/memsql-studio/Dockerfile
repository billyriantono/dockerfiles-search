FROM centos:6.8

ENV RELEASE_CHANNEL=production \
    STUDIO_VERSION=1.9.4

RUN yum -y install yum-security
RUN yum -y update-minimal --setopt=tsflags=nodocs --security --sec-severity=Important --sec-severity=Critical \
    && yum install -y yum-utils procps \
    && yum-config-manager --add-repo https://release.memsql.com/${RELEASE_CHANNEL}/rpm/x86_64/repodata/memsql.repo \
    && yum clean all

RUN yum install -y \
    memsql-studio-${STUDIO_VERSION} \
    && yum clean all

ENTRYPOINT ["memsql-studio"]
