FROM jenkins/jenkins:lts

USER root
RUN echo "Europe/Paris" > /etc/timezone && dpkg-reconfigure -f noninteractive tzdata
RUN curl -sL https://deb.nodesource.com/setup_7.x | bash -
RUN curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add -
RUN echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list
RUN apt-get update
RUN apt-get install -y apt-utils nodejs build-essential yarn && wget https://repo1.maven.org/maven2/org/flywaydb/flyway-commandline/4.1.2/flyway-commandline-4.1.2-linux-x64.tar.gz && tar -xvf flyway-commandline-4.1.2-linux-x64.tar.gz && rm flyway-commandline-4.1.2-linux-x64.tar.gz
USER jenkins
