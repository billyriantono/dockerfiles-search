FROM golang:1.11.4

RUN curl https://glide.sh/get | sh
RUN curl -sL https://deb.nodesource.com/setup_10.x | bash -
RUN apt-get update
RUN apt-get install -y build-essential
RUN apt-get install -y nodejs
RUN npm rebuild node-sass --force
RUN curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add - && \
    echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list && \
    apt update && apt-get install -y yarn
RUN go get -u github.com/alecthomas/gometalinter
RUN gometalinter --install
