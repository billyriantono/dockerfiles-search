FROM amazon/dynamodb-local
EXPOSE 8000
VOLUME ["/data"]
WORKDIR /home/dynamodblocal
ENTRYPOINT ["java", "-Djava.library.path=./DynamoDBLocal_lib", "-jar", "DynamoDBLocal.jar", "-dbPath", "/data"]
