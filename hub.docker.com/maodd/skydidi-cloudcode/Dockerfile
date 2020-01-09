FROM alpine
	
RUN apk update && apk add --no-cache git


ARG GITHUB_TOKEN

RUN echo TOKEN ${GITHUB_TOKEN}

RUN git clone https://maodd:${GITHUB_TOKEN}@github.com/parsegroundapps/pg-app-hvh4ysk1eye9uiecrbt88d0eupvspy.git /parse

VOLUME /parse/cloud

RUN apk del git

WORKDIR /parse
