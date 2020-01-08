FROM brcomconcretesolutions/jenkins-build-bitbucket

USER root

RUN apt-get -y update
RUN apt-get install -y ruby ruby-dev bundler
RUN apt-get clean
RUN gem install aws-sdk

USER jenkins
