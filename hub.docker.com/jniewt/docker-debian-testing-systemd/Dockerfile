FROM debian:testing

ENV DEBIAN_FRONTEND noninteractive

# Install dependencies.
RUN apt-get update \
    && apt-get install -y --no-install-recommends \
       sudo \
       python \
    && rm -rf /var/lib/apt/lists/* \
    && rm -Rf /usr/share/doc && rm -Rf /usr/share/man \
    && apt-get clean

RUN apt-get update && apt-get install -y systemd
COPY systemctl.py /usr/bin/systemctl
RUN chmod +x /usr/bin/systemctl

