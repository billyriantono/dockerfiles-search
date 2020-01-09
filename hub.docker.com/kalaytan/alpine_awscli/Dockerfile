FROM alpine:latest
RUN apk -v --update \
	add python \
    py-pip
RUN pip install --upgrade pip
RUN pip install --upgrade --no-cache-dir awscli 
RUN apk -v --purge del py-pip && \
    rm /var/cache/apk/*
RUN apk -v --update add git bash
RUN git config --global user.email "docker@example.com" && \
	git config --global user.name "Docker"
VOLUME /app
WORKDIR /app