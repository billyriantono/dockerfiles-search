FROM swaggerapi/swagger-ui
LABEL maintainer="Vitaly Kovalyshyn"

ENV WEBITEL_MAJOR 19.12
ENV WEBITEL_REPO_BASE https://github.com/webitel

RUN apk add curl && mkdir /app
COPY run.sh /app/run.sh

CMD ["sh", "/app/run.sh"]
