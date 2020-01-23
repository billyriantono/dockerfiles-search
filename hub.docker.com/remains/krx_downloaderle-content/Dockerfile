FROM python:alpine

RUN apk add --no-cache curl
RUN pip install connexion[swagger-ui] 

RUN mkdir /spec
ADD run.sh /spec

WORKDIR /spec

EXPOSE 5000

ENTRYPOINT ["./run.sh"]
