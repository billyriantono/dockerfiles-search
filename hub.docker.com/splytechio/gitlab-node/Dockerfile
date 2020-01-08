FROM gitlab/dind

MAINTAINER splytechio

ENV TERM xterm
ENV DEBIAN_FRONTEND noninteractive

# Initial setup
RUN apt-get update && \
    apt-get install -y -qq --no-install-recommends git unzip && \
    apt-get autoremove -y && \
    apt-get clean all

# Google Cloud SDK
ENV PATH /google-cloud-sdk/bin:$PATH
RUN wget https://dl.google.com/dl/cloudsdk/channels/rapid/google-cloud-sdk.zip && \
    unzip google-cloud-sdk.zip && \
    rm google-cloud-sdk.zip && \
    google-cloud-sdk/install.sh \
        --usage-reporting=true \
        --path-update=true \
        --bash-completion=true \
        --rc-path=/.bashrc \
        --additional-components app kubectl alpha beta app-engine-go bigtable && \
    google-cloud-sdk/bin/gcloud config set --installation component_manager/disable_update_check true && \
    sed -i -- 's/\"disable_updater\": false/\"disable_updater\": true/g' /google-cloud-sdk/lib/googlecloudsdk/core/config.json

WORKDIR /app
ENV PATH $PATH:/app
COPY package.json package-lock.json /app/

RUN curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.33.8/install.sh | bash && \
    \. "$HOME/.nvm/nvm.sh" && \
    nvm install stable && ln -sf $(which node) /usr/local/bin/node && \
    npm i -g concurrently && ln -sf $(which concurrently) /usr/local/bin/concurrently && \
    npm i

COPY bin /app
COPY entrypoint.sh /entrypoint.sh

ENTRYPOINT ["/entrypoint.sh"]
