FROM ubuntu:18.04

ENV DEBIAN_FRONTEND=noninteractive
RUN apt-get update && apt-get install --yes --no-install-recommends \
        mingw-w64 \
        make \
        flex \
        bison \
        pandoc \
        texlive-latex-extra \
        texlive-fonts-recommended \
        lmodern \
        libx11-6 \
        xxd \
        libxext6 \
        libxft2 \
        libxss1 \
        tcl-dev \
        xvfb \
        gcc \
        libc6-dev \
        git-core \
        unzip \
        zip \
        sudo \
    && rm --recursive --force /var/lib/apt/lists/*

ADD https://phoenixnap.dl.sourceforge.net/project/freewrap/freewrap/freeWrap%206.64/freewrap664.tar.gz /tmp
ADD https://phoenixnap.dl.sourceforge.net/project/freewrap/freewrap/freeWrap%206.64/freewrap664.zip /tmp
ADD http://david.zemon.name:8111/repository/download/OpenSpin_LinuxX8664/.lastSuccessful/openspin.tar.gz!/openspin?guest=1 /usr/local/bin

RUN mkdir /opt/freewrap \
    && tar -xf /tmp/freewrap664.tar.gz -C /opt/freewrap \
    && rm /tmp/freewrap664.tar.gz \
    && unzip -o /tmp/freewrap664.zip -d /opt/freewrap \
    && rm /tmp/freewrap664.zip \
    && chmod +x /usr/local/bin/openspin

ENV HOME=/home/captain
RUN groupadd --gid 1000 captain \
  && useradd --home-dir "${HOME}" --uid 1000 --gid 1000 captain \
  && mkdir --parents "${HOME}/.ssh" \
  && cp /root/.bashrc /root/.profile "${HOME}" \
  && chown --recursive captain:captain "${HOME}" \
  && chmod --recursive 777 "${HOME}" \
  && echo "ALL ALL=NOPASSWD: ALL" >> /etc/sudoers

COPY start.sh /start.sh
ENTRYPOINT ["/start.sh"]
