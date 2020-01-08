FROM alpine:edge

ENV CARGO_HOME=/usr/local/cargo

RUN apk add --no-cache \
		cargo \
		gcc \
		musl-dev \
		postgresql-dev \
		rust \
	&& mkdir -p $CARGO_HOME \
	&& chmod a+w $CARGO_HOME

ENV PATH="$CARGO_HOME/bin:$PATH"
