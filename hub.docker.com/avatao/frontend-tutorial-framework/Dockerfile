FROM avatao/debian:buster

RUN curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg     |\
    sudo apt-key add -                                   &&\
    echo "deb https://dl.yarnpkg.com/debian/ stable main" |\
    sudo tee /etc/apt/sources.list.d/yarn.list           &&\
    apt-get update                                       &&\
    apt-get install -y --no-install-recommends nodejs yarn &&\
    rm -rf /var/lib/apt/lists/*

WORKDIR /srv

COPY . /srv
RUN yarn install --frozen-lockfile --network-timeout 1000000 && yarn build --no-progress

CMD yarn start
