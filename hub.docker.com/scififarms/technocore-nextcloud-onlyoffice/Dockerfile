FROM onlyoffice/documentserver:5.4.0.21
# 
#RUN apk add --no-cache [ANY DESIRED PACKAGE]
#
### Set up the CMD as well as the pre and post hooks.
COPY go-init /bin/go-init
COPY entrypoint.sh /usr/bin/entrypoint.sh
COPY exitpoint.sh /usr/bin/exitpoint.sh
#
ENTRYPOINT ["go-init"]
CMD ["-main", "/usr/bin/entrypoint.sh /app/onlyoffice/run-document-server.sh", "-post", "/usr/bin/exitpoint.sh"]
