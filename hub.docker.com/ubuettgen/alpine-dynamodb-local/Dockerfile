FROM ubuettgen/alpine-openjdk-jre-base 
MAINTAINER Ulrich Büttgen  "ulrich@buettgen.org"

#add a starter script to the image (and create the folder) 
ADD dynamodb.sh /opt/dynamodb-local/

#  cwd to our brand new folder
WORKDIR /opt/dynamodb-local

RUN wget http://dynamodb-local.s3-website-us-west-2.amazonaws.com/dynamodb_local_latest -O dynamodb-local.tgz
RUN tar xzf dynamodb-local.tgz && rm -f dynamodb-local.tgz

EXPOSE 8000

ENTRYPOINT ["./dynamodb.sh"]

