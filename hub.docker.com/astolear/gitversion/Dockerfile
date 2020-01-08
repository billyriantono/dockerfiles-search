FROM mono:5.8
LABEL authors="Artur Stolear <artur.stolear@gmail.com>"

ENV GITVERSION 3.6.5

# Install gitversion tools
RUN apt-get update && apt-get install unzip \
    && curl -L https://github.com/GitTools/GitVersion/releases/download/v${GITVERSION}/GitVersion_${GITVERSION}.zip -o tmp.zip \
    && unzip tmp.zip -d /tmp/git-version \
    && mv /tmp/git-version /usr/local/bin/git-version/ \
    && rm tmp.zip

RUN echo '#!/bin/bash\nexec mono /usr/local/bin/git-version/GitVersion.exe "$@"' > /usr/bin/git-version && chmod +x /usr/bin/git-version