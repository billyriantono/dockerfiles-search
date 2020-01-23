FROM dlord/minecraft:java8

RUN curl -SL -o /tmp/atm3.zip https://media.forgecdn.net/files/2756/981/ATM3-5.12.3_Server-FULL.zip \
    && cd /opt/minecraft \
    && unzip /tmp/atm3.zip \
    && chmod +x ServerStart.sh \
    && ./ServerStart.sh -a -i \
    && find . -name "*.log" -exec rm -rf {} \; \
    && rm /tmp/atm3.zip

ENV MINECRAFT_STARTUP_JAR=forge-1.12.2-14.23.5.2838-universal.jar \
    MINECRAFT_VERSION=1.12.2
