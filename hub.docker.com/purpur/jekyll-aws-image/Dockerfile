# Build:
#   docker build -t purpur/rumdorado .
#
# Use:
#    docker run -v $(pwd):/data -it purpur/rumdorado /bin/bash
#
# Use this image both locally and/or in your pipeline
#
# === run as part of build/locally
# RUN bundler install
# RUN jekyll build
# RUN aws s3 sync ./_site s3://www.rumdorado.com/ --acl public-read  --delete


FROM jekyll/jekyll:pages

RUN apk update
RUN apk add --upgrade curl
RUN apk add --update python
RUN apk add --update unzip

RUN apk add python-dev

RUN gem install bundler
# RUN bundler install

#          - jekyll build
#          - ls -la


RUN curl "https://s3.amazonaws.com/aws-cli/awscli-bundle.zip" -o "/tmp/awscli-bundle.zip"

RUN ls -la /tmp

RUN unzip /tmp/awscli-bundle.zip -d /tmp/awscli/
RUN /tmp/awscli/awscli-bundle/install -i /usr/local/aws -b /usr/local/bin/aws

WORKDIR /data

#          - aws s3 ls
#          - aws s3 sync ./_site s3://www.rumdorado.com/ --acl public-read  --delete

#ADD Gemfile
#ADD Gemfile.lock

# === run as part of build
# RUN bundler install
# RUN jekyll build
# RUN aws s3 sync /data/_site s3://www.rumdorado.com/ --acl public-read  --delete

