FROM debian:stable-slim
EXPOSE 8080
# Deps
RUN apt-get update && apt-get install -y git curl gnupg
RUN curl -sL https://deb.nodesource.com/setup_9.x | bash -
RUN curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add -
RUN echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list
RUN apt-get update
RUN apt-get install -y yarn nodejs

# Kiwi
WORKDIR /app
RUN git clone https://github.com/kiwiirc/kiwiirc.git
WORKDIR /app/kiwiirc
RUN yarn install
RUN yarn run build

