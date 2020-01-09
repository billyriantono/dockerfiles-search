FROM ubuntu:18.04

ENV SDKMAN_DIR="/usr/local/sdkman"

SHELL ["/bin/bash","-c"]
RUN apt-get update; \
    apt-get install -y curl zip unzip vim; \
    apt-get clean;

RUN curl -s "https://get.sdkman.io" | bash

#Change the sdkman setting to enable installation in slient mode
RUN sed -i -e 's/sdkman_auto_answer=false/sdkman_auto_answer=true/' ${SDKMAN_DIR}/etc/config

CMD ["bash"]