FROM alpine:3.8

LABEL maintainer GitterDone

#docker run -ti --rm -v ${PWD}:/cloudsend <file> https://<nextcloud url>/index.php/s/yFYQE43KXtq6SHB

RUN apk --update --no-cache add curl bash && \
    rm -rf /var/lib/apt/lists/* 

VOLUME /cloudsend
WORKDIR /cloudsend

RUN curl -o '/bin/cloudsend.sh' 'https://gist.githubusercontent.com/GitterDoneScott/84f6fb0bd5b1fc18cc0025cf53c0020a/raw/90c540313a7f1737d368ca8c8dffe3e296fed318/cloudsend.sh' && chmod +x /bin/cloudsend.sh

ENTRYPOINT ["/bin/cloudsend.sh"]
CMD ["-h"]
