FROM ubuntu:18.04

RUN apt-get update && \
    apt-get install -y git wget tar make g++ python3 python3-pip && \
    apt-get clean

RUN mkdir -p /server/analysis
COPY ./app /app

ENTRYPOINT [ "/bin/bash", "/app/run.sh" ]
CMD [ "--test" ]

EXPOSE 443
EXPOSE 80

