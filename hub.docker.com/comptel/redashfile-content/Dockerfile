FROM swaggerapi/swagger-ui:latest

LABEL MAINTAINER="codeontap"

RUN apk add zip 

RUN mkdir /app/
RUN mkdir /app/indir/
RUN mkdir /app/outdir/

ADD ./scripts/docker-export.sh /usr/share/nginx/

CMD ["sh", "/usr/share/nginx/docker-export.sh"]