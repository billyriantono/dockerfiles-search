FROM alpine:3.4
MAINTAINER dalongrong
# Install base packages
RUN apk update && apk add curl bash tree tzdata \
    && cp -r -f /usr/share/zoneinfo/Hongkong /etc/localtime \
    && apk del tzdata
CMD ["/bin/bash"]
