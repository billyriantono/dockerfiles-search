FROM ej52/alpine-node:6.9
MAINTAINER kotiesmit@gmail.com

RUN \
  apk --update add openjdk7-jre curl && \
  curl -o /tmp/dynamo.tar.gz -L http://dynamodb-local.s3-website-us-west-2.amazonaws.com/dynamodb_local_latest && \
  tar xvzf /tmp/dynamo.tar.gz && \
  rm -rf third_party_licenses LICENSE.txt && \
  apk --purge del curl

EXPOSE 8000
CMD ["java", "-Djava.library.path=./DynamoDBLocal_lib", "-jar", "./DynamoDBLocal.jar"]
