FROM aihara/geodjangobase:py3.6

ENV DOCKERIZE_VERSION v0.5.0

RUN apk add --update ca-certificates openssl && update-ca-certificates
RUN apk add --no-cache --virtual .dev gcc g++ make linux-headers postgresql-dev git libpng libjpeg-turbo-dev zlib-dev musl-dev libffi-dev
RUN [ ! -f /usr/local/bin/dockerize ] && wget https://github.com/jwilder/dockerize/releases/download/$DOCKERIZE_VERSION/dockerize-linux-amd64-$DOCKERIZE_VERSION.tar.gz && tar -C /usr/local/bin -xzvf dockerize-linux-amd64-$DOCKERIZE_VERSION.tar.gz && rm dockerize-linux-amd64-$DOCKERIZE_VERSION.tar.gz
CMD /bin/sh