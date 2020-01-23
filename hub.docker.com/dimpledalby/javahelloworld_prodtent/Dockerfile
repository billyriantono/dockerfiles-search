FROM alpine:3.8
RUN apk update
RUN apk add python 
RUN apk add py-pip
RUN pip install jinja2
RUN pip install requests
RUN mkdir /working
WORKDIR /working
ENTRYPOINT [ "python" ]