FROM swift:5.1.2-bionic
LABEL maintainer="Bryan Flood <bryanfloodcontact@gmail.com>"
LABEL description="🐳 Simple Dev Environment for Serverside Swift using 💧Vapor 4"
LABEL url="https://github.com/KnowledgePending/Vapor-4-Docker"
RUN apt-get -qq update                             && \
    apt-get -qq install git zlib1g-dev             && \
    git clone https://github.com/vapor/toolbox.git && \
    cd toolbox                                     && \
    git checkout 18.0.0-beta.19                    && \
    swift build -c release --disable-sandbox       && \
    mv .build/release/vapor /usr/local/bin