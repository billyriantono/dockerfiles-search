FROM kovan/node

RUN apk add --update git build-base python

WORKDIR /
ADD run.sh .

EXPOSE 3000

CMD ["/run.sh"]
