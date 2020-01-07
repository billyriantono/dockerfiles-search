FROM python:3.7.3-alpine3.10

LABEL maintainer="lework <lework@yeah.net>"


ARG WORKSPACE=/src

ENV WORKSPACE=${WORKSPACE} \
    TIMEZONE=Asia/Shanghai
	

RUN apk --update -t --no-cache add tzdata curl \
    && ln -snf /usr/share/zoneinfo/${TIMEZONE} /etc/localtime \
    && echo "${TIMEZONE}" > /etc/timezone \
    \
	&& apk add --no-cache --virtual .build-deps \
	gcc \
	libc-dev \
	linux-headers \
	&& pip install uwsgi \
	&& apk del --no-network .build-deps

WORKDIR ${WORKSPACE}

EXPOSE 80

CMD ["sh", "-c", "uwsgi -y ${WORKSPACE}/uwsgi.yml"]