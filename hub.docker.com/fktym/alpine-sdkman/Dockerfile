FROM frolvlad/alpine-glibc:alpine-3.9

ENV SDKMAN_DIR=/root/.sdkman

RUN apk upgrade --update && \
    apk add --no-cache --update libstdc++ curl ca-certificates bash zip unzip openssl shadow 

RUN chsh -s /bin/bash

RUN curl -s "https://get.sdkman.io" | bash

RUN echo "sdkman_auto_answer=true" > $SDKMAN_DIR/etc/config && \
    echo "sdkman_auto_selfupdate=false" >> $SDKMAN_DIR/etc/config && \
    echo "sdkman_insecure_ssl=true" >> $SDKMAN_DIR/etc/config

ENTRYPOINT ["/bin/bash"]
