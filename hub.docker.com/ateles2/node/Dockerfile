FROM phusion/baseimage:0.10.1

RUN apt-get update

# nodejs
RUN curl -sL https://deb.nodesource.com/setup_8.x | bash -
RUN apt-get install -y nodejs git

# yarn
RUN curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add -
RUN echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list
RUN apt-get update && apt-get install yarn

# cleanup
RUN apt-get clean && rm -rf /var/lib/apt/lists/* && apt-get autoremove -y

RUN groupmod -g 1000 www-data && usermod -u 1000 www-data

RUN useradd tomcat && groupmod -g 500 tomcat && usermod -u 500 tomcat
