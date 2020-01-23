########## OS ##########
FROM elixir:1.4

RUN apt-get update
RUN apt-get -y install mariadb-client
RUN apt-get -y install subversion

RUN curl -sL https://deb.nodesource.com/setup_6.x | bash -
RUN apt-get install -y nodejs
RUN apt-get install -y build-essential
