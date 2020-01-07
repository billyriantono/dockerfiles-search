FROM bash
LABEL maintainer "Tanja84DK <tanja84dk@gmail.com>" architecture="AMD64/x86_64"

# Install Software
RUN apk add --no-cache --update ffmpeg && \
    rm -f /var/cache/apk/* && \
    mkdir /scripts/
    

# Setup Configuration

COPY M4V-Converter.sh default.conf LICENSE README.md /scripts/

ENTRYPOINT ["bash", "/scripts/M4V-Converter.sh", "-o", "/Output", "-i", "/Input"]
