FROM ubuntu:latest

MAINTAINER Amit Kumar Jaiswal <amitkumarj441@gmail.com>

COPY BlockchainInGolang .
RUN chmod +x BlockchainInGolang && apk add --no-cache curl
EXPOSE 80/tcp
CMD [ "./BlockchainInGolang" ]
