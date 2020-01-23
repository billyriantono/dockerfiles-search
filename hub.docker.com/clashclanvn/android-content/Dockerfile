FROM buildkite/agent:2

RUN apk --no-cache add bash gawk sed grep bc coreutils jq \
	groff less python py-pip && \
	mkdir -p /aws && \
	pip install awscli
