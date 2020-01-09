FROM python:3.8
RUN apt-get update && \
    apt-get install -y \
        libavdevice-dev \
        libavfilter-dev \
        libopus-dev \
        libvpx-dev \
        libsrtp2-dev \
        ffmpeg \
        pkg-config && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*
RUN wget -q -O /usr/local/bin/gosu \
        "https://github.com/tianon/gosu/releases/download/1.11/gosu-$(dpkg --print-architecture | awk -F- '{ print $NF }')" && \
    chmod +x /usr/local/bin/gosu

COPY requirements.txt /
RUN pip install -r /requirements.txt

COPY . /package
RUN cd /package && python ./setup.py install

VOLUME /data
RUN groupadd --system witness
RUN useradd --system witness --gid witness --shell /bin/bash --home-dir /data

COPY entrypoint.sh /
ENTRYPOINT ["/entrypoint.sh"]
