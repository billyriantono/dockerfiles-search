FROM fluent/fluentd:v0.12

RUN apk update \
 && apk --no-cache add ca-certificates openssl git \
 && update-ca-certificates

ENV DOCKERIZE_VERSION v0.3.0
RUN wget https://github.com/jwilder/dockerize/releases/download/$DOCKERIZE_VERSION/dockerize-linux-amd64-$DOCKERIZE_VERSION.tar.gz \
 && tar -C /usr/local/bin -xzvf dockerize-linux-amd64-$DOCKERIZE_VERSION.tar.gz \
 && rm dockerize-linux-amd64-$DOCKERIZE_VERSION.tar.gz

RUN gem install fluent-plugin-elasticsearch \
  && gem install fluent-plugin-aws-elasticsearch-service 

COPY ./templates/fluent.tmpl /etc/fluent/fluent.tmpl

ENTRYPOINT ["dockerize", "-template", "/etc/fluent/fluent.tmpl:/etc/fluent/fluent.conf"]
CMD ["fluentd", "-c", "/etc/fluent/fluent.conf", "-vv"]
