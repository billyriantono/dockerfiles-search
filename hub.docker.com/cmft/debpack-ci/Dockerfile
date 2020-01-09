FROM debian:unstable


# Install packages
RUN apt-get update && apt-get install --fix-missing -y \
        #general tools
        git \
        # packaging tools
        build-essential \
        devscripts \
        dh-make \
        dh-virtualenv \
        git-buildpackage \
        lintian \
        pkg-config \
        piuparts \
        procps \ 
        python-pysvn \
        python-git \
        python-mock \
        python-stdeb \
        docker.io

# Install setuptools2uglydeb ALBA package
COPY setuptools2uglydeb_0.3.1a0+git20180419.1.d00e15-0~bpo9+0~alba+1_all.deb /tmp
RUN dpkg -i /tmp/setuptools2uglydeb_0.3.1a0+git20180419.1.d00e15-0~bpo9+0~alba+1_all.deb

