FROM webcenter/openjdk-jre:8

MAINTAINER	Dmitry Gopkalo <dmitry.gopkalo@tonicforhealth.com>


# Update distro and install OpenJDK8-jre-headless
RUN apt-get update && \
    apt-get install curl zip -y && \
    apt-get clean all && \
    rm -rf /var/lib/apt/lists/*


RUN cd /usr/local/lib && \
    curl -L -sS https://github.com/antonwierenga/activemq-cli/releases/download/v0.1.0/activemq-cli-0.1.0.zip > activemq-cli.zip && \
    unzip activemq-cli.zip && \
    mv activemq-cli-0.1.0 activemq-cli && \
    rm activemq-cli.zip && \
    ln -s $(pwd)/activemq-cli/bin/activemq-cli /usr/local/bin/activemq-cli

COPY enter.sh /usr/local/bin/

RUN chmod +x /usr/local/bin/enter.sh

ENTRYPOINT ["enter.sh"]


CMD ["help"]