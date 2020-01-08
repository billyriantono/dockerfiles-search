FROM markadams/chromium-xvfb

WORKDIR /usr/src/app
USER root
RUN apt-get update
RUN apt-get install -y gpg \
    && curl -sL https://deb.nodesource.com/setup_10.x | bash - \
    && apt-get install -y nodejs gpg \
    && rm -rf /var/lib/apt/lists