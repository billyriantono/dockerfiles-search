FROM choasia/gradle-node-webapp-image:gradle-5.6.4

ENV DEBIAN_FRONTEND noninteractive
RUN apt update -y && apt install -y awscli

ENTRYPOINT ["/bin/bash", "--login"]
