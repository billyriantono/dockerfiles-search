FROM alpine
LABEL repo github.com/WpTestLabs/SvrStkCtrl
LABEL maintainer WpTestLabs <_____@gmail.com>

RUN apk --update add curl git jq openssh rsync nano \ 
      pwgen haveged    py-pip && \
    pip install s3cmd   zip unzip && \
    rm -rf /var/lib/apt/lists/* && \
    rm /var/cache/apk/*

#COPY /DkrBldCtx/a.txt /a.txt

CMD /bin/sh
