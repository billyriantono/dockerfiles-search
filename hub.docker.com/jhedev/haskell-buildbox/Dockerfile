FROM haskell:7.8

MAINTAINER joel.hermanns@gmail.com

RUN apt-get update
RUN apt-get install -y curl git

RUN bash -c "`curl -sL https://raw.githubusercontent.com/buildbox/agent/master/install.sh`"

CMD /root/.buildbox/buildbox-agent start --access-token $ACCESS_TOKEN