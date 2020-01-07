FROM ubuntu:18.04
MAINTAINER k0kubun

# node-gyp build crashes with nodejs v10, so using nodejs v8.
# gnupg is needed to `apt-key add`. curl is needed to fetch pubkey.
# "python" and "make"/"g++" (build-essential) are needed to install node-gyp.
# gcc/g++-multilib are needed to build 32bit packages and require --no-install-recommends.
# wine and wine32 are used for building Windows packages. wine32 requires `dpkg --add-architecture i386`.
# git is used by bower. zip is used at Nocturn's travis.

RUN apt-get update && apt-get install -y curl gnupg && \
  curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add - && \
  echo "deb https://dl.yarnpkg.com/debian/ stable main" > /etc/apt/sources.list.d/yarn.list && \
  dpkg --add-architecture i386 && apt-get update && apt-get install -y --no-install-recommends \
  nodejs npm yarn python git zip build-essential \
  gcc-multilib g++-multilib wine-stable wine32 && \
  apt-get clean && rm -rf /var/lib/apt/lists/*
