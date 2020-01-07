FROM redis:alpine

# Get bash, curl, openssl, zip
RUN apk update && apk upgrade && \
    apk add --no-cache bash openssl curl zip

# Install aws-cli
RUN apk -Uuv add groff less python py-pip
RUN pip install --upgrade pip
RUN pip install awscli
RUN apk --purge -v del py-pip

# Create app directory
RUN mkdir -p /usr/src/app
WORKDIR /usr/src/app
COPY . /usr/src/app

# Set timezone to UTC by default
RUN ln -sf /usr/share/zoneinfo/Etc/UTC /etc/localtime

EXPOSE 7000 7001 7002 7003 7004 7005

CMD [ "sh", "startCluster.sh"]