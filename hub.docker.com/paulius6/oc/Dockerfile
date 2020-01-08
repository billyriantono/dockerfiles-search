FROM centos:7.5.1804

ENV VER v3.11.0
ENV PKG openshift-origin-client-tools-${VER}-0cbc58b-linux-64bit.tar.gz
ENV URL https://github.com/openshift/origin/releases/download/${VER}/${PKG}

RUN set -x \
    && yum install -y \
        curl \
    && yum clean all \
    && curl -LO ${URL} \
    && tar zxvf ${PKG}  \
    && mv openshift-*${VER}*/oc /usr/bin/ \
    && rm -rf openshift*

CMD ["oc"]
