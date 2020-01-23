FROM alpine
MAINTAINER Aaron D Borden <adborden@a14n.net>

RUN apk --no-cache add \
  git \
  python \
  py-pip

RUN pip install awsebcli

CMD ["eb", "--version"] 
