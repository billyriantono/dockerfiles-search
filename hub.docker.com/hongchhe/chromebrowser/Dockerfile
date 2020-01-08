FROM       hongchhe/ubuntu-python3
MAINTAINER Hongchuang <hehongchuang@hotmail.com>

RUN        sed -i "s/cn.archive/archive/g" /etc/apt/sources.list \
        && apt-get update \
        && apt-get install -y wget \
        && wget -q -O - https://dl-ssl.google.com/linux/linux_signing_key.pub | apt-key add - \
        && echo 'deb [arch=amd64] http://dl.google.com/linux/chrome/deb/ stable main' | tee /etc/apt/sources.list.d/google-chrome.list \
        && apt-get update \
        && apt-get install -y google-chrome-stable
RUN        sed -i "s/archive.ubuntu/cn.archive.ubuntu/g" /etc/apt/sources.list \
        && pip install --upgrade pip \
        && pip install selenium

