# Maven (3 with JDK 11) and AWS CLI
# This image is mainly for performing builds and deployments.

## Builder for AWS CLI
FROM maven:3-jdk-11 AS build-awscli

RUN set -eux; \
	mkdir -p /tmp/awscli; \
	curl -fSL -o "/tmp/awscli/awscli-bundle.zip" "https://s3.amazonaws.com/aws-cli/awscli-bundle.zip"; \
	unzip "/tmp/awscli/awscli-bundle.zip" -d "/tmp/awscli/"; \
	/tmp/awscli/awscli-bundle/install --install-dir "/usr/local/aws/"; \
	rm -rf /tmp/awscli

## Final Image
FROM maven:3-jdk-11 AS image

RUN set -eux; \
	mkdir /usr/local/aws

COPY --from=build-awscli /usr/local/aws/ /usr/local/aws/

RUN set -eux; \
	ln -s /usr/local/aws/bin/aws /usr/local/bin/aws
