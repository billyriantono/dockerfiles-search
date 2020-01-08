FROM n4nn31355/android-studio

USER root

#nodejs
RUN apt-get update && \
    apt-get install -y curl && \
    curl -sL https://deb.nodesource.com/setup_7.x | sudo -E bash - && \
    apt-get install -y nodejs

#react-native-cli
RUN npm install -g react-native-cli

#watchman
RUN apt-get update && apt-get install -y git automake make gcc python-dev
RUN git clone https://github.com/facebook/watchman.git && cd watchman && \
    git checkout v4.7.0 && \
    ./autogen.sh && \
    ./configure && \
    make && \
    make install && \
    rm -rf /var/lib/apt/lists/*

USER $CUSTOMUSER
