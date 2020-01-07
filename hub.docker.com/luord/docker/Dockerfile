FROM alpine

RUN apk --no-cache add nodejs nodejs-npm && adduser -D app

USER app

ENV HOME=/home/app
ENV PATH=${PATH}:${HOME}/.npm-packages/bin
RUN echo 'prefix=${HOME}/.npm-packages' > ${HOME}/.npmrc && mkdir ${HOME}/default

WORKDIR ${HOME}/default

CMD node
