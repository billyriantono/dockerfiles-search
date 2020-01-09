FROM openjdk:8-jdk-alpine
LABEL maintainer="Stav Shamir <shamir.stav@gmail.com>"

RUN apk -q --update add fontconfig ttf-dejavu bash git

RUN wget -q -O /intellij-2018.2.tar.gz https://download.jetbrains.com/idea/ideaIC-2018.3.tar.gz && \
    mkdir -p /usr/share/intellij && \
    tar -xf /intellij-2018.2.tar.gz --strip-components=1 -C /usr/share/intellij && \
    rm /intellij-2018.2.tar.gz

CMD /usr/share/intellij/bin/idea.sh
