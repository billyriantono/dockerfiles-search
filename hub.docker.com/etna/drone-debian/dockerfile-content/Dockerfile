FROM etheleon/docker-alpine-python-machinelearning

RUN apk add --no-cache py-psycopg2
RUN pip install --upgrade awscli==1.14.5 s3cmd==2.0.1 python-magic && \
    rm /var/cache/apk/*

