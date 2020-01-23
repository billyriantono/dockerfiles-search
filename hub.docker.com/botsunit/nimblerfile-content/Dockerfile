FROM boro/nodejs:latest
MAINTAINER boro <docker@bo.ro>

RUN apk add make gcc g++ python linux-headers paxctl gnupg
RUN pip install ansible

CMD ["/start.sh"]