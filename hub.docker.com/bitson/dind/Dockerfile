FROM docker:dind

RUN apk add --no-cache py-pip bash
RUN pip install docker-compose

ENTRYPOINT ["dockerd-entrypoint.sh"]
CMD []