FROM ubuntu:16.04

ENV LANG C.UTF-8
ENV TZ America/New_York

RUN apt-get update && \
    apt-get dist-upgrade -y && \
    apt-get install -y --no-install-recommends default-jdk && \
    ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && \
        echo $TZ > /etc/timezone && \
        dpkg-reconfigure -f noninteractive tzdata && \
        apt-get autoremove -y && apt-get clean && \
        rm -rf /var/lib/apt/lists/*

ENV JAVA_HOME /usr/lib/jvm/default-java/

CMD ["bash"]
