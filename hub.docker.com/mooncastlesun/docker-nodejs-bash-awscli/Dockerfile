FROM mesosphere/aws-cli:1.14.5
RUN \
 apk -v --update add \
  bash \
  coreutils \
  curl \
  findutils \
  libmagic \
  rsync \
  py-pip \
  nodejs \
  nodejs-npm \
 && \
 pip install --upgrade python-magic boto boto3 && \
 npm i -g yarn@0.27.5 && \
 apk -v --purge del py-pip && \
 rm /var/cache/apk/* && \
 curl -o /usr/bin/s3-parallel-put https://raw.githubusercontent.com/mishudark/s3-parallel-put/master/s3-parallel-put && \
 chmod 755 /usr/bin/s3-parallel-put
ENTRYPOINT ["/bin/bash"]
