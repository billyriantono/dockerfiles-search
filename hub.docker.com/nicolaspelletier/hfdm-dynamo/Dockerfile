FROM centos:7.6.1810

# Some metadata.
MAINTAINER "marc.poirier@autodesk.com"
LABEL maintainer="marc.poirier@autodesk.com"

# Create our main application folder.
RUN mkdir -p opt/dynamodb
WORKDIR /opt/dynamodb

# Download and unpack dynamodb.
RUN archive=dynamodb_local_2018-04-11.tar.gz \
 && curl -L http://dynamodb-local.s3-website-us-west-2.amazonaws.com/${archive} -o ${archive} \
 && echo "8993dc016b22471db6a071dc46dc54aa67c95e05  ${archive}" | sha1sum -c \
 && tar -zxf ${archive} \
 && rm -f ${archive}

# Install OpenJDK 8 JRE
RUN yum install -y java-1.8.0-openjdk

# Install pip and boto3 using pip
RUN curl https://bootstrap.pypa.io/get-pip.py -o get-pip.py \
 && python get-pip.py \
 && rm -f get-pip.py \
 && pip install boto3==1.9.108

# The entrypoint is the dynamodb jar. Default port is 8000.
EXPOSE 8000
CMD ["/opt/pod/boot.sh"]

# Specific to HFDM
COPY scripts/hfdm/*.py ./scripts/hfdm/

# Common
COPY scripts/boot.sh /opt/pod/
COPY scripts/*.py ./scripts/

RUN bash -c "/opt/pod/boot.sh && java -jar DynamoDBLocal.jar & (python ./scripts/hfdm/setup.py)"
