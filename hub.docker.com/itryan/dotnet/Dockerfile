FROM microsoft/dotnet
MAINTAINER itryan <itechryan@gmail.com>
RUN mkdir -p ~/projects && cd ~/projects \
 && apt-get update \
 && apt-get install -y rsync \
 && rm -rf /var/lib/apt/lists/*