FROM java:8
MAINTAINER Steve Sloka <slokas@upmc.edu>

RUN mkdir /opt/dynamodb_local
RUN wget -q -O - http://dynamodb-local.s3-website-us-west-2.amazonaws.com/dynamodb_local_latest.tar.gz | tar -xzf - -C /opt/dynamodb_local

WORKDIR /opt/dynamodb_local

EXPOSE 8000

ENTRYPOINT ["java", "-Djava.library.path=/opt/dynamodb_local/DynamoDBLocal_lib", "-jar", "DynamoDBLocal.jar", "-sharedDb"]
