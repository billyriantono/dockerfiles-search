FROM ubuntu:14.04
COPY bin /opt/bin
COPY data /tmp
ENV TERM "xterm"
RUN chmod +x /opt/bin/build.sh && sleep 1 && /opt/bin/build.sh \
&&  sleep 1 && rm -f /opt/bin/build.sh
