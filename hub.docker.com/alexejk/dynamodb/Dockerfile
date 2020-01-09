FROM alexejk/java8:latest

# Update the system and ensure CA certificates are installed and then cleanup
# Create WORKDIR, download & unpack dynamodb to it and cleanup again
RUN apk update && \
    apk upgrade && \
    apk add wget && \
    apk add ca-certificates && \
    rm -rf /var/cache/apk/* && \
    mkdir -p /opt/dynamodb && \
    wget http://dynamodb-local.s3-website-us-west-2.amazonaws.com/dynamodb_local_latest.tar.gz -q -P /opt/dynamodb/ && \
    tar -xzf /opt/dynamodb/dynamodb_local_latest.tar.gz -C /opt/dynamodb

WORKDIR /opt/dynamodb

# Default port is 8000 for dynamodb
EXPOSE 8000

# Standard way of starting dynamodb
ENTRYPOINT ["java", "-jar", "DynamoDBLocal.jar"]