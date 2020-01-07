FROM python:3.5-alpine
ENV PYTHONUNBUFFERED 1

RUN apk --update add \
	gcc \
	git \
	linux-headers \
	make \
	musl-dev \
	nginx \
	openssl \
	postgresql-client \
	postgresql-dev \
	supervisor \
	&& rm -rf /var/cache/apk/*

RUN mkdir -p /etc/supervisor.d/

EXPOSE 8000

CMD ["supervisord", "-n"]
