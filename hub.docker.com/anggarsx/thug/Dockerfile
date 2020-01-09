FROM ubuntu:19.10

RUN apt-get update && \
    apt-get install -y software-properties-common apt-utils locales tzdata

RUN echo "tzdata tzdata/Areas select Asia" > timezone.txt
RUN echo "tzdata tzdata/Zones/Asia select Jakarta" >> timezone.txt
RUN debconf-set-selections timezone.txt
RUN rm /etc/timezone
RUN rm /etc/localtime
RUN dpkg-reconfigure -f noninteractive tzdata

RUN apt-get update && apt-get install -y \
    apt-utils \
    bash \
    curl \
    figlet \
    gcc \
    g++ \
    git \
    sudo \
    aria2 \
    util-linux \
    libffi-dev \
    libwebp-dev \
    libxml2 \
    libxml2-dev \
    libxslt-dev \
    musl \
    neofetch \
    openssl \
    postgresql \
    postgresql-client \
    openssl \
    pv \
    jq \
    wget \
    python \
    python3 \
    python3-dev \
    python3-pip \
    sqlite \
    ffmpeg \
    sudo \
    python-dev \
    speedtest-cli \
    iputils-ping \
    net-tools \
    libc6 \
    libcap2 \
    libidn2-0 \
    libnettle6

RUN git clone https://anggarsx@bitbucket.org/anggarsx/thuggbot.git -b sgb /root/bot
WORKDIR /root/bot/

COPY ./emilia/config.py /root/bot/emilia/

#
# Install requirements
#
RUN pip3 install -r requirements.txt
CMD ["python3","-m","emilia"]
