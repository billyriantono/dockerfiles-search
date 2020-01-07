FROM alpine:3.8

MAINTAINER Isaac Gittins

WORKDIR /stacks

RUN apk add --no-cache python3

RUN pip3 install --no-cache --upgrade pip
RUN pip3 install --no-cache stacker yamllint python-dateutil==2.8.0

ENTRYPOINT ["stacker"]
CMD ["-h"]
