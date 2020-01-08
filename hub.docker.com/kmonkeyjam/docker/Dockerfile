FROM openjdk:8-jre

RUN /usr/bin/curl -L https://s3-us-west-2.amazonaws.com/dynamodb-local/dynamodb_local_latest.tar.gz | /bin/tar xz

ENTRYPOINT ["/usr/bin/java", "-Djava.library.path=./DynamoDBLocal_lib", "-jar", "DynamoDBLocal.jar"]

EXPOSE 8000

CMD ["-dbPath", "/var/dynamodb_local", "-port", "8000", "-sharedDb"]

VOLUME ["/var/dynamodb_local"]
