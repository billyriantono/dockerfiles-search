FROM elasticsearch:5.6

ENV NODE_OPTIONS=--max_old_space_size=4096

# install node && elasticdump
RUN curl -sL https://deb.nodesource.com/setup_10.x | bash - \
  && apt-get install -y nodejs \
  && npm install elasticdump -g

WORKDIR /tmp
