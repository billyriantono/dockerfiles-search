FROM docker:latest

RUN apk add git \
	python3 \
	py3-setuptools \
	alpine-sdk \
	jq \
		&& pip3 install --no-cache-dir awscli \
		&& pip3 install awsebcli --upgrade

ENTRYPOINT ["sh"]
