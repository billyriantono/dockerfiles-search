FROM alpine:3.9

ENV GitSecretsVersion=1.3.0

WORKDIR /
RUN mkdir -p /git-secrets /app && \
	wget -O /${GitSecretsVersion}.tar.gz https://github.com/awslabs/git-secrets/archive/${GitSecretsVersion}.tar.gz && \
	tar xvzf /${GitSecretsVersion}.tar.gz --strip 1 -C /git-secrets && \
    cp /git-secrets/git-secrets /bin/ && \
    rm -rf /git-secrets

ENTRYPOINT [ '/bin/git-secrets' ]
