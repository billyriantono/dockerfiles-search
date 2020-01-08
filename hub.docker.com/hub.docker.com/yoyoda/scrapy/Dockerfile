FROM python:alpine

RUN apk add build-base
RUN apk add libffi-dev
RUN apk add libxml2-dev
RUN apk add openssl-dev
RUN apk add libxslt-dev
RUN pip install scrapy
RUN pip install scrapyd
RUN pip install scrapyd-client

VOLUME ["/spiders"]
EXPOSE 6800
COPY scrapyd.conf /etc/scrapyd/

#ENTRYPOINT ["scrapy"]
#CMD ["shell"]

CMD ["scrapyd"]
