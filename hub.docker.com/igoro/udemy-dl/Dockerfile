# Usage example:
# docker run -it --rm -v "$PWD:/udemy" udemy-dl https://www.udemy.com/a-course-in-your-profile/
FROM python:3-alpine

RUN apk add --update build-base linux-headers libxml2 libxml2-dev libxslt libxslt-dev libjpeg-turbo libjpeg-turbo-dev aria2 && \
  pip install udemy-dl==0.2.2a1 && \
  apk del build-base linux-headers libxml2-dev libxslt-dev libjpeg-turbo-dev && \
  rm -rf /var/cache/apk/*

RUN mkdir /udemy
WORKDIR /udemy

ENTRYPOINT ["udemy-dl"]
