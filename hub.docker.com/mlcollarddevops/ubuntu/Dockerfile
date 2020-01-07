FROM ubuntu:19.04
LABEL edu.uanet.collard-devops.url="https://github.com/mlcollard/sortDevOps" \
      edu.uanet.collard-devops.distro="ubuntu" \
      edu.uanet.collard-devops.osversion="19.04" \
      edu.uanet.collard-devops.architecture="x86_64"

RUN apt-get update && apt-get install --no-install-recommends -y \
    g++ \
    make \
    && rm -rf /var/lib/apt/lists/*
