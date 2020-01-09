FROM alpine:edge

ENV	NMAP_VERSION 7.40-r0
RUN	apk --no-cache add \
		nmap=$NMAP_VERSION \
		nmap-scripts=$NMAP_VERSION \
		nmap-nselibs=$NMAP_VERSION

ENTRYPOINT ["nmap"]
