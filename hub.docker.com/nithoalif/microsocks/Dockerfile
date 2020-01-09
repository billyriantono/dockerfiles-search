FROM alpine:3.10 AS builder
COPY . /src
WORKDIR /src
RUN apk add --no-cache build-base \
	&& make

FROM alpine:3.10
COPY --from=builder /src/microsocks /usr/bin/microsocks
ENTRYPOINT ["/usr/bin/microsocks"]
