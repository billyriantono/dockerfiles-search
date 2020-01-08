FROM debian

RUN apt-get update
RUN apt-get install -y curl gnupg gnupg1 gnupg2
RUN curl -sL https://deb.nodesource.com/setup_10.x | bash -
RUN apt-get install -y nodejs

EXPOSE 3000
