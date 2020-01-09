FROM swaggerapi/swagger-ui
LABEL maintainer="me@dotronglong.com"

ENV UI_CSS="swagger-ui.css"

RUN apk add --update unzip curl
RUN curl -SLO https://github.com/ostranme/swagger-ui-themes/archive/develop.zip \
	&& unzip develop.zip && rm -rf develop.zip \
	&& mv swagger-ui-themes-develop/themes /usr/share/nginx/html/ \
	&& rm -rf swagger-ui-themes-develop

ADD ./start.sh /usr/share/nginx/start.sh
CMD ["sh", "/usr/share/nginx/start.sh"]