FROM alpine

RUN apk update && \
      apk add jq socat bash git python3 vim && \
      rm -vrf /var/cache/apk/*

ADD ./ /home/rest
WORKDIR /home/rest

RUN ln -s /home/rest/odroid/init_servo.sh /bin/servo

ARG PORT

ENV PORT $PORT
EXPOSE $PORT

ENV SHELL /bin/bash
ENV PATH $PATH:$SHELL

ENTRYPOINT ./index.sh && /bin/bash
