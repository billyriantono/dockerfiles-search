FROM atlassian/default-image:2

RUN echo 'debconf debconf/frontend select Noninteractive' | debconf-set-selections \
    && apt-get update \
    && apt-get upgrade -y \
    && apt-get install -y \
        python3-pip jq \
    && apt-get clean \
    && pip3 install awscli --no-cache-dir
