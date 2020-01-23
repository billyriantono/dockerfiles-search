FROM alpine:3.8
RUN apk update
RUN apk add jq
RUN apk add python 
RUN apk add py-pip
RUN apk add curl
RUN pip install yq

RUN mkdir /working
WORKDIR /working
ENTRYPOINT [ "python" ]