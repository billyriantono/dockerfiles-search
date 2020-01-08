##################################################################################################
# venuusaur/venuu-os:build-*
##################################################################################################

FROM alpine:3.4

RUN apk update
RUN apk add \
      openssh \
      ca-certificates \
      git

ENV GIT_LFS_VERSION=2.3.4 GIT_LFS_SHA256=6755e109a85ffd9a03aacc629ea4ab1cbb8e7d83e41bd1880bf44b41927f4cfe

RUN apk add curl && \
    curl -sLO https://github.com/github/git-lfs/releases/download/v$GIT_LFS_VERSION/git-lfs-linux-amd64-$GIT_LFS_VERSION.tar.gz && \
    sha256sum git-lfs-linux-amd64-$GIT_LFS_VERSION.tar.gz | grep $GIT_LFS_SHA256 && \
    tar zxvf git-lfs-linux-amd64-$GIT_LFS_VERSION.tar.gz && \
    mv git-lfs-$GIT_LFS_VERSION/git-lfs /usr/bin/ && \
    rm -rf git-lfs-$GIT_LFS_VERSION && \
    rm -rf git-lfs-linux-amd64-$GIT_LFS_VERSION.tar.gz && \
    apk del curl
