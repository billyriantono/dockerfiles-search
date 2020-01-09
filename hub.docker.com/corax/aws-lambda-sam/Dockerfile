FROM python:3.6.6-alpine3.8

RUN apk add --no-cache gcc libc-dev && \
	pip install --user aws-sam-cli && \
	apk del gcc libc-dev && \
	rm -rf /var/cache/apk/*

ENV PATH="/root/.local/bin/:${PATH}"
WORKDIR /var/opt
EXPOSE 3000
ENTRYPOINT ["/root/.local/bin/sam"]