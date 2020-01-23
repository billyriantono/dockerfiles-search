FROM imatic/docker-node-dev:12

ENV JOKER_VERSION="0.12.7" CLJ_VERSION="1.10.0.442"

RUN apt-get update && \
    apt-get install -y unzip && \
    # lein
    curl --output /usr/local/bin/lein https://raw.githubusercontent.com/technomancy/leiningen/stable/bin/lein && \
    chmod +x /usr/local/bin/lein && \
    lein && \
    # clj
    curl -O https://download.clojure.org/install/linux-install-${CLJ_VERSION}.sh && \
    chmod +x linux-install-${CLJ_VERSION}.sh && \
    ./linux-install-${CLJ_VERSION}.sh && \
    rm ./linux-install-${CLJ_VERSION}.sh && \
    # joker
    wget -O /opt/joker.zip https://github.com/candid82/joker/releases/download/v${JOKER_VERSION}/joker-${JOKER_VERSION}-linux-amd64.zip && \
    mkdir -p /opt/joker && \
    unzip /opt/joker.zip -d /opt/joker && \
    mv /opt/joker/joker /usr/local/bin/joker && \
    # cleanup
    rm -rf /var/lib/apt/lists/*
