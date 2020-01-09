FROM centos:7

RUN curl -sL https://rpm.nodesource.com/setup_10.x | bash -
RUN yum install -y -q nodejs
RUN yum install -y -q git

RUN alias cnpm="npm --registry=https://registry.npm.taobao.org \
--cache=$HOME/.npm/.cache/cnpm \
--disturl=https://npm.taobao.org/dist \
--userconfig=$HOME/.cnpmrc"

RUN npm install -g pm2

VOLUME /var/app
WORKDIR /var/app

EXPOSE 3000

ENTRYPOINT [ "pm2", "start", "--no-daemon", "--name=app"]
CMD ["?"]

