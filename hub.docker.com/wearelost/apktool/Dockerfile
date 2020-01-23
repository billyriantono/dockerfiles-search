FROM java:8-jre

WORKDIR /

RUN wget https://raw.githubusercontent.com/iBotPeaches/Apktool/master/scripts/linux/apktool && \
    wget https://bitbucket.org/iBotPeaches/apktool/downloads/apktool_2.3.4.jar -O apktool.jar && \
    chmod u+x /apktool

WORKDIR /apk

ENTRYPOINT ["/apktool"]
