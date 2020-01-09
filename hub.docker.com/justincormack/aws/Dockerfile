FROM alpine

RUN apk update && apk add py-pip groff less
RUN pip install awscli

ENTRYPOINT ["aws"]
