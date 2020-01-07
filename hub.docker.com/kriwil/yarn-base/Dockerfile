FROM ubuntu:18.04
RUN apt-get update
RUN apt-get install -y curl netbase gnupg gnupg2 gnupg1
RUN curl -sL https://deb.nodesource.com/setup_11.x | bash -
RUN curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add -
RUN echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list
RUN apt-get update
RUN apt-get install -y nodejs yarn
RUN apt-get clean -y

