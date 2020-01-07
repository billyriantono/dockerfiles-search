FROM jetbrains/teamcity-agent:latest

MAINTAINER Aleksei Chernov <kot.lex@gmail.com>

RUN curl -sL https://deb.nodesource.com/setup_8.x | bash - \
    && apt-get update && apt-get install -y nodejs sudo \ 
    && curl -sS http://cdn.sencha.com/cmd/6.5.3/no-jre/SenchaCmd-6.5.3-linux-amd64.sh.zip > /tmp/sencha.zip \
    && unzip /tmp/sencha.zip -d /tmp \
    && sudo -u buildagent /tmp/SenchaCmd*.sh -q --all

ENV PATH /home/buildagent/bin/Sencha/Cmd/:$PATH
