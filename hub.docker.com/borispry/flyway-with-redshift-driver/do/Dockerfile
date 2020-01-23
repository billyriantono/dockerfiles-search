FROM ubuntu:bionic

RUN apt-get update -q && \
    apt-get install --no-install-recommends -qy \
                        curl unzip openjdk-8-jdk && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN mkdir -p /playgo
ADD https://blueplane.s3-eu-west-1.amazonaws.com/playgo/PlayGo_4.0_21122015_linux.gtk_64bit.zip /playgo/PlayGo_4.0.zip
COPY wrappedUnzip.sh /usr/bin
RUN cd /playgo && \
    chmod +x /usr/bin/wrappedUnzip.sh && \
    wrappedUnzip.sh PlayGo_4.0.zip && \
    chmod +x PlayGo_4.0_21122015_linux.gtk_64bit/playgo
VOLUME /workspace
ENTRYPOINT [ "/playgo/PlayGo_4.0_21122015_linux.gtk_64bit/playgo" ]
