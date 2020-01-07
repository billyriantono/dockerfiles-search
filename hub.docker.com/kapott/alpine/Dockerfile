#
# Kapott's Alpine Baseimage
#

FROM alpine:latest
MAINTAINER kapott <kapott@aivd.33mail.com>

# Install root filesystem
ADD ./root /

# Install base packages
RUN apk add --no-cache curl wget bash && \
    echo -ne "Alpine Linux 3.8 image. (`uname -rsv`)\n" >> /root/.built

# Define bash as default command
CMD ["/bin/bash"]