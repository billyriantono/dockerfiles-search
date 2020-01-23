FROM ubuntu:18.04
LABEL maintainer "Adam Bozson <adam@bozson.io>"

RUN apt-get update && apt-get install -y \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg2 \
    software-properties-common \
    --no-install-recommends

WORKDIR /tmp
RUN apt-get update && apt-get -y install module-init-tools libglvnd-dev wget \
    && wget http://uk.download.nvidia.com/XFree86/Linux-x86_64/435.21/NVIDIA-Linux-x86_64-435.21.run \
    && chmod u+x NVIDIA-Linux-x86_64-435.21.run \
    && ./NVIDIA-Linux-x86_64-435.21.run -a --ui=none --no-kernel-module --no-questions

RUN curl -s https://brave-browser-apt-release.s3.brave.com/brave-core.asc \
    | apt-key --keyring /etc/apt/trusted.gpg.d/brave-browser-release.gpg add - \
    && . /etc/os-release \
    && echo "deb [arch=amd64] https://brave-browser-apt-release.s3.brave.com/ $UBUNTU_CODENAME main" \
    | tee /etc/apt/sources.list.d/brave-browser-release-${UBUNTU_CODENAME}.list \
    && apt-get update && apt-get install -y brave-browser

COPY local.conf /etc/fonts/local.conf
COPY ttf /usr/share/fonts/truetype/
RUN apt-get install -y fonts-noto-color-emoji && fc-cache -f -v

RUN apt-get install -y pulseaudio --no-install-recommends
COPY pulseaudio.client.conf /etc/pulse/client.conf

RUN add-apt-repository -y ppa:dyatlov-igor/la-capitaine && \
    apt-get install -y la-capitaine-cursor-theme

RUN groupadd -g 1000 brave-user \ 
    && useradd --no-log-init -rm -u 1000 -g 1000 brave-user
USER brave-user
ENV LANG en-GB

ENTRYPOINT ["brave-browser"]
CMD ["--no-sandbox", "--ignore-gpu-blacklist", "--test-type"]

