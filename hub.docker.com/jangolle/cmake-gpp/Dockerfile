FROM alpine:latest

LABEL maintainer="elijah.zakirov@gmail.com"

RUN apk update && apk upgrade
RUN apk add --no-cache \
	g++ \
	gcc \
	clang \
	make \
	cmake \
	git \
	bash

CMD ["/bin/bash"]

