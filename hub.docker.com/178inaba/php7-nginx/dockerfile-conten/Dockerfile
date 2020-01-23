# :: Header
FROM ubuntu:18.04
ARG DEBIAN_FRONTEND=noninteractive
ENV signalCliVersion=0.6.3

# :: Run
USER root
RUN groupadd -g 1000 signal \
    && useradd -rm -d /home/signal -s /bin/bash -g signal -u 1000 signal
RUN mkdir --p /signal/var \
    && chmod 700 /signal/var \
    && mkdir -p /home/signal/.local/share/signal-cli
RUN apt-get update -y \
    && apt-get install default-jre wget -y
RUN wget -qO - https://github.com/AsamK/signal-cli/releases/download/v${signalCliVersion}/signal-cli-${signalCliVersion}.tar.gz | tar xvzf - -C /opt \
    && mv /opt/signal-cli-${signalCliVersion} /opt/signal-cli \
    && ln -s /opt/signal-cli/bin/signal-cli /usr/local/bin/signal-cli \
    && ln -s /signal/var /home/signal/.local/share/signal-cli/data

# :: Version
RUN echo "CI/CD{{$(signal-cli -v 2>&1)}}"

# :: docker -u 1000:1000 (no root initiative)
RUN chown -R signal:signal \
    /signal \
    /opt/signal-cli \
    /home/signal/.local/share/signal-cli

# :: Volumes
VOLUME ["/signal/var"]

# :: Start
USER signal