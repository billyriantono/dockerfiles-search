FROM alpine:3.5

MAINTAINER konmeo

RUN apk add -U ca-certificates
RUN mv /etc/profile.d/color_prompt /etc/profile.d/color_prompt.sh && \
    chmod a+x /etc/profile.d/color_prompt.sh

COPY aliases.sh /etc/profile.d/

USER nobody
CMD sed -n '/PRETTY_NAME/s/.*="\(.*\)"/\1/p' /etc/os-release && uname -srm
