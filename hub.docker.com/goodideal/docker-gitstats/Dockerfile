FROM alpine:3.6

RUN apk add --no-cache python git gnuplot
ADD ./ /gitstats
WORKDIR /git

CMD ["/gitstats/start.sh"]