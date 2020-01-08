FROM alpine:3.6

RUN mkdir -p /nsqmail
COPY data/* /nsqmail/
RUN chmod +x /nsqmail/nsqmail
WORKDIR /nsqmail

CMD ["/nsqmail/nsqmail"]