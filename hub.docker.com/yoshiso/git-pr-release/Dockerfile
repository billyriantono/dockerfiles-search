FROM ruby:2.3-alpine


RUN gem install git-pr-release

RUN apk --no-cache add git openssh-client

ADD run /bin/run
WORKDIR /workspace

RUN mkdir /root/.ssh && echo 'Host *' > /root/.ssh/config && echo '  StrictHostKeyChecking no' >> /root/.ssh/config

ENTRYPOINT ["run"]

