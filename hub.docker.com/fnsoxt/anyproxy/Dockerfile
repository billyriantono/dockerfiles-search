FROM n0trace/yarn
LABEL maintainer="fnsoxt@gmail.com"

COPY rootCA.* /root/.anyproxy/certificates/

RUN yarn global add anyproxy &&\
    yarn cache clean

EXPOSE 8001 8002

ENTRYPOINT anyproxy --intercept --ws-intercept
