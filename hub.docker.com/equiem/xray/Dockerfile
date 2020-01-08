FROM equiem/node-build-tools

EXPOSE 2000/udp

RUN curl -o daemon.zip https://s3.dualstack.us-east-2.amazonaws.com/aws-xray-assets.us-east-2/xray-daemon/aws-xray-daemon-linux-2.x.zip && \
    unzip daemon.zip -d /usr/bin

ENTRYPOINT [ "/usr/bin/xray" ]
CMD [ "-b", "0.0.0.0:2000", "-o" ]
