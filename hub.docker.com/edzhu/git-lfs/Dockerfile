FROM ubuntu:latest
LABEL maintainer="edward.zr.zhu@gmail.com"

RUN apt-get update && apt-get install -y curl && \
    curl -s https://packagecloud.io/install/repositories/github/git-lfs/script.deb.sh | bash && \
    apt-get update && apt-get install -y git-lfs && \
    git lfs install && \
    rm -rf /var/lib/apt/lists/*