FROM microsoft/aspnet:1.0.0-rc1-update1-coreclr

RUN apt-get install curl && \
    curl -sL https://deb.nodesource.com/setup_4.x | bash - && \
    apt-get install -y nodejs && \
    npm set progress=false && \
    npm install -g gulp@3.9.1 && \
    npm install -g bower@1.7.7
