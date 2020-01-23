FROM ibmjava:8-sdk

# CMD ["gradle"]

RUN apt-get update && apt-get install --yes --no-install-recommends git
RUN git clone https://github.com/dipendub/distledger.git

RUN set -o errexit -o nounset \
    && groupadd --system --gid 1000 gradle \
    && useradd --system --gid gradle --uid 1000 --shell /bin/bash --create-home gradle \
    && mkdir /home/gradle/.gradle \
    && chown --recursive gradle:gradle /home/gradle \
    && ln -s /home/gradle/.gradle /root/.gradle

VOLUME /home/gradle/.gradle

WORKDIR /home/gradle

RUN apt-get install unzip

RUN set -o errexit -o nounset \
    && wget --no-verbose --output-document=gradle.zip "https://services.gradle.org/distributions/gradle-4.4-bin.zip" \
    && unzip gradle.zip \
    && rm gradle.zip \
    && mv gradle-4.4 /opt/gradle/ \
    && ln --symbolic /opt/gradle/bin/gradle /usr/bin/gradle

#    && gradle --version

WORKDIR /distledger

ENV JAVA_OPTS=""
ENV WALLET="-PappArgs=sync --wallet=/distledger/random.wallet --net=TEST --mode=SPV --chain=/distledger/random.chain"
ENTRYPOINT [ "sh", "-c", "gradle --no-daemon wallet_tool $WALLET" ]
# ENTRYPOINT [ "sh", "-c", "gradle --version" ]