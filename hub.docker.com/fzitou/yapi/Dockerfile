FROM node:alpine as build

ENV YAPI_VERSION v1.8.4
ENV YAPI_DOWNLOAD_URL https://github.com/YMFE/yapi/archive/${YAPI_VERSION}.tar.gz

RUN apk add -U --no-cache \
        curl \
        tar \
        git \
        python \
        make \
        openssl \
        gcc \
        bash \
    && curl -sSLO ${YAPI_DOWNLOAD_URL} \
    && mkdir yapi \
    && tar -zxvf ${YAPI_VERSION}.tar.gz -C ./yapi  --strip-components 1 \
    && cd yapi \
    && npm install --production


FROM node:alpine

MAINTAINER jzitou@gmail.com

ENV HOME /yapi/vendors/

COPY --from=build /yapi/ ${HOME}

WORKDIR ${HOME}

EXPOSE 3000

ENTRYPOINT ["node"]

CMD ["server/app.js"]