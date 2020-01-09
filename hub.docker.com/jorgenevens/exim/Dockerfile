FROM alpine

RUN apk --no-cache add exim

ENTRYPOINT ["exim"]
CMD ["-bdf", "-q15m", "-v"]
