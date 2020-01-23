FROM swift:4.1
LABEL maintainer="Bryan Flood <bryanfloodcontact@gmail.com>"
LABEL description="🐳 Simple Dev Environment for Serverside Swift using 💧Vapor"
LABEL url="https://github.com/KnowledgePending/Vapor-Docker"
RUN apt-get -qq update                      && \
    apt-get -qq install wget                && \
    wget -qO- https://apt.vapor.sh | bash;
RUN apt-get -qq install vapor
