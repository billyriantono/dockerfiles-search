# build:
#   docker build -t st2/allinone $HOME/dockerfiles/st2-allinone/
# debug:
#   docker run -it --rm=true --name=st2 --hostname=st2 --entrypoint=bash st2/allinone

FROM ubuntu:14.04

ADD mongod.init /etc/init.d/mongod

# ST2 password
ENV ST2_PASSWORD=changeme

RUN export DEBIAN_FRONTEND=noninteractive \
&& export NO_PROXY=localhost,127.0.0.1,${HOSTNAME} \
&& apt-get update \
&& apt-get dist-upgrade --yes \
&& apt-get install --yes curl vim gnupg-curl openssh-server \
&& /etc/init.d/rsyslog start \
&& /etc/init.d/ssh start \
&& curl -sSL -O https://stackstorm.com/packages/install.sh \
&& chmod +x install.sh \
&& ./install.sh --user=st2admin --password=${ST2_PASSWORD} \
&& echo "stanley:stanley" | chpasswd \
&& rm -f /install.sh /st2-community-installer.sh /st2bootstrap-deb.sh \
&& apt-get clean \
&& rm -rf /var/lib/apt/lists/*

ADD start_st2.sh /

ENTRYPOINT /start_st2.sh
