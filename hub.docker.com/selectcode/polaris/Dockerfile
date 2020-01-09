FROM alpine
MAINTAINER "Florian Baader <florian.baader@selectcode.de>"
RUN apk add wget --no-cache
RUN wget https://github.com/FairwindsOps/polaris/releases/download/0.4.0/polaris_0.4.0_Linux_x86_64.tar.gz -O - | tar -xz -C /usr/local/bin/ && chmod +x /usr/local/bin/polaris
