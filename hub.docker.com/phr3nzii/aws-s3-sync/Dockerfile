FROM alpine:latest

RUN apk add --no-cache python3 && \
    python3 -m ensurepip && \
    pip3 install --no-cache --upgrade awscli pip

ENV SYNC_OPTIONS ""

CMD echo "Running aws s3 sync s3://$SOURCE_BUCKET/ s3://$DESTINATION_BUCKET/ $SYNC_OPTIONS" && aws s3 sync s3://$SOURCE_BUCKET/ s3://$DESTINATION_BUCKET/ $SYNC_OPTIONS
