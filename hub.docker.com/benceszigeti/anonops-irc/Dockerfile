FROM alpine:edge
MAINTAINER Bence Szigeti <bence.szigeti@gohyda.com>

RUN apk add --update-cache --no-cache \
    python \
    tor \
    weechat \
    weechat-perl \
    weechat-python

ARG USERNAME=user
RUN addgroup ${USERNAME} \
    && adduser -D -s /sbin/nologin -G ${USERNAME} ${USERNAME}
ENV HOME /home/${USERNAME}
WORKDIR ${HOME}
ADD entrypoint.sh ${HOME}/
RUN chmod +x ${HOME}/entrypoint.sh
RUN chown -R ${USERNAME}:${USERNAME} ${HOME}/

USER ${USERNAME}
ENTRYPOINT ["./entrypoint.sh"]
