FROM mdillon/postgis:9.5-alpine

RUN apk --update add python curl unzip && \
    cd /tmp && \
    curl "https://s3.amazonaws.com/aws-cli/awscli-bundle.zip" -o "awscli-bundle.zip" && \
    unzip awscli-bundle.zip && \
    ./awscli-bundle/install -i /usr/local/aws -b /usr/local/bin/aws && \
    rm awscli-bundle.zip && \
    rm -rf awscli-bundle && \
    mkdir -p /sql-data-init-files

COPY *.sh /

ENTRYPOINT ["/entrypoint.sh"]

CMD ["postgres"]