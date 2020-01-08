FROM alpine:3.5

RUN apk add --no-cache nginx \
	&& rm -rf /var/cache/apk/* /usr/include

EXPOSE 80 443

CMD ["nginx", "-g", "daemon off;"]

