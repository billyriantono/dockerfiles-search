FROM scality/s3server:6018536a as intermediate

# Some metadata.
MAINTAINER "nicolas.pelletier@autodesk.com"
LABEL maintainer="nicolas.pelletier@autodesk.com"

# Install the aws client.
RUN printf "deb http://archive.debian.org/debian/ jessie main\ndeb-src http://archive.debian.org/debian/ jessie main\ndeb http://security.debian.org jessie/updates main\ndeb-src http://security.debian.org jessie/updates main" > /etc/apt/sources.list \
  && apt-get update \
  && apt-get install -y python --no-install-recommends \
  && curl https://bootstrap.pypa.io/ez_setup.py | python \
  && curl https://bootstrap.pypa.io/get-pip.py | python \
  && pip install awscli

# Start the container and add the buckets to it.
ENV AWS_ACCESS_KEY_ID=accessKey1
ENV AWS_SECRET_ACCESS_KEY=verySecretKey1

COPY docker/start_and_populate.sh .
COPY docker/populate.sh .

RUN ./start_and_populate.sh

# Copy the database to the final image.
FROM scality/s3server:6018536a

COPY --from=intermediate /usr/src/app/myFavoriteDataPath /usr/src/app/myFavoriteDataPath
COPY --from=intermediate /usr/src/app/myFavoriteMetadataPath /usr/src/app/myFavoriteMetadataPath

ENV S3DATAPATH="/usr/src/app/myFavoriteDataPath"
ENV S3METADATAPATH="/usr/src/app/myFavoriteMetadataPath"
