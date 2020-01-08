FROM docker
MAINTAINER Aleksander Heintz <alxandr@alxandr.me>

# Add mos tool
ADD build.sh /usr/local/bin/run-build
RUN chmod +x /usr/local/bin/run-build
ADD https://mongoose-os.com/downloads/mos-2.5.1/linux/mos /usr/local/bin/
RUN chmod +x /usr/local/bin/mos

# Add volume and workdir
VOLUME /workspace
VOLUME /build
WORKDIR /workspace

# Set entrypoint
ENTRYPOINT [ "run-build" ]
