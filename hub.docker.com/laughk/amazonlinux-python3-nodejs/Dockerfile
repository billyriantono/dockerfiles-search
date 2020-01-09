FROM amazonlinux:2018.03

RUN curl -LO https://rpm.nodesource.com/setup_8.x && \
    echo "dbe7dc4713984caaa96092b827fd149e setup_8.x" | md5sum -c - && \
    /bin/sh setup_8.x && \
    mkdir -m 777 -pv /.npm /.config && \
    yum -y install \
        gcc \
        gcc-c++ \
        mysql56 \
        mysql56-devel \
        python36 \
        python36-devel \
        git \
        gettext \
        nodejs \
        bzip2
