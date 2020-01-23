FROM kalilinux/kali-linux-docker
# Metadata params
ARG BUILD_DATE
ARG VERSION
ARG VCS_URL
ARG VCS_REF

LABEL org.label-schema.build-date=$BUILD_DATE \
      org.label-schema.vcs-url=$VCS_URL \
      org.label-schema.vcs-ref=$VCS_REF \
      org.label-schema.version=$VERSION \
      org.label-schema.name='Kali Linux' \
      org.label-schema.description='Kali Linux docker image' \
      org.label-schema.usage='https://www.kali.org/news/official-kali-linux-docker-images/' \
      org.label-schema.url='https://www.kali.org/' \
      org.label-schema.vendor='Offensive Security' \
      org.label-schema.schema-version='1.0' \
      org.label-schema.docker.cmd='docker run --rm kalilinux/kali-linux-docker' \
      org.label-schema.docker.cmd.devel='docker run --rm -ti kalilinux/kali-linux-docker' \
      org.label-schema.docker.debug='docker logs $CONTAINER' \
      io.github.offensive-security.docker.dockerfile="Dockerfile" \
      io.github.offensive-security.license="GPLv3" \
      MAINTAINER="0303ff"
RUN echo "deb http://http.kali.org/kali kali-rolling main contrib non-free" > /etc/apt/sources.list && \
    echo "deb-src http://http.kali.org/kali kali-rolling main contrib non-free" >> /etc/apt/sources.list
ENV DEBIAN_FRONTEND noninteractive
RUN set -x \
    && apt-get -yqq update \
    && apt-get -yqq dist-upgrade \
    && apt-get clean \
    && apt-get -yqq install kali-tools-headless \
    && apt-get -yqq install netcat skipfish tmux python3 python3-pip sshuttle golang \
    && python3 -m pip install sslyze cheat requests \
    && git clone https://gist.github.com/3990d70d64026f29aba6fe7593aeda9e.git \
    && mv 3990d70d64026f29aba6fe7593aeda9e/.bashrc ~/ \
    && rm -r 3990d70d64026f29aba6fe7593aeda9e \
    && git clone https://github.com/1N3/Sn1per.git \
    && cd Sn1per \
    && sed '/This script will/d' install.sh > new_install.sh \
    && mv new_install.sh install.sh \
    && sed '/read answer/d' install.sh > new_install.sh \
    && mv new_install.sh install.sh \
    && sh install.sh \
    && cd .. \
    && rm -r Sn1per \
    && mkdir /root/.cheat \
    && cd /root/.cheat \
    && wget https://gist.githubusercontent.com/tilt41/5eb09f2fcbffe1ea3da6eacc730c42e0/raw/6adc3e87c88672bcd60ff8abe71d77f9ae132498/reneg \
    && wget https://gist.githubusercontent.com/tilt41/e1308d00dc0ffde706fe9adbf20755fb/raw/8dc7e06d8ebdd65015d47d8b629c829e8b718e0f/xst \
    && wget https://gist.githubusercontent.com/tilt41/8e9e4ddd5041a36e11147e011e3267ea/raw/f874389284d073389f2ab614baafd840a830698a/xss \
    && mkdir /root/toolz \
    && cd /root/toolz \
    && git clone https://github.com/eldraco/domain_analyzer.git \
    && git clone https://github.com/1N3/XSSTracer.git \
    && git clone https://github.com/m4ll0k/WAScan.git \
    && git clone https://github.com/s0md3v/XSStrike.git \
    && git clone https://github.com/hahwul/a2sv.git \
    && git clone https://github.com/andresriancho/nimbostratus.git \
    && git clone https://github.com/maaaaz/webscreenshot.git \
    && git clone --depth 1 https://github.com/drwetter/testssl.sh.git \
    && go get -u github.com/zricethezav/gitleaks \
    && mv /root/go/bin/* /usr/local/bin/ \
    && rm -r /root/go
CMD ["bash"]
