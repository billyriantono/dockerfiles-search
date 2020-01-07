FROM nginx
RUN apt-get update -y && \
    apt-get install -y curl \
                       libcurl3 \
                       libcurl3-dev \
                       ngrep \
                       gnupg

RUN curl -sL https://deb.nodesource.com/setup_6.x | bash -
RUN apt-get install -y nodejs
RUN apt-get install -y build-essential

CMD [ "node" ]
