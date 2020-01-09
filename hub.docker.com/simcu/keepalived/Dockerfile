FROM alpine:edge
COPY run.sh /run.sh
RUN apk add --update keepalived && \
 	rm -rf /var/cache/apk/* && \
 	chmod +x /run.sh
CMD /run.sh