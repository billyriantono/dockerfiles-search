FROM philippwaller/debian:latest

LABEL org.label-schema.schema-version="1.0" \
	  org.label-schema.name="Golang" \
	  org.label-schema.description="The Go Programming Language"

ENV GOPATH=/usr/local

RUN apt-get update \
 && apt-get install -y golang-go \
 && rm -rf /var/lib/apt/lists/* /tmp/*

ENTRYPOINT ["bash"]
CMD ["pwd"]
