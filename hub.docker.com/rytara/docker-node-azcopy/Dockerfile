FROM microsoft/dotnet:2.0-sdk

RUN apt-get update && \
    apt-get install -y wget curl gnupg rsync&& \
    curl -sL https://deb.nodesource.com/setup_8.x | bash && \
    apt-get install -y nodejs && \
    apt-get install -y build-essential && \
    wget -O azcopy.tar.gz https://aka.ms/downloadazcopyprlinux && \
    tar -xf azcopy.tar.gz && \
    ./install.sh 


# RUN node -v
# RUN npm -v
# RUN which azcopy
