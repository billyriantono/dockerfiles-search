FROM debian:stretch

MAINTAINER larry.shen@nxp.com

WORKDIR /root

# install necessary software
RUN set -eux; \
  apt-get update && \
  apt-get install minicom -y && \
  apt-get install python -y && \
  apt-get install python-pip -y && \
  pip install tornado==4.5.1 && \
  apt-get install git -y && \
  git clone --depth=1 https://github.com/liftoff/GateOne.git && \
  apt-get purge git -y && \
  cd GateOne && \
  python setup.py install && \
  cd && \
  rm -fr GateOne && \
  apt-get install openssh-server -y && \
  apt-get install expect -y && \
  apt-get autoremove -y

# add scripts
RUN mkdir -p /rdebug/users

ADD ./entrypoint.sh entrypoint.sh
RUN chmod 775 ./entrypoint.sh
ADD ./menu.sh /etc/skel/
RUN chmod 775 /etc/skel/menu.sh
ADD ./serial /etc/skel/

ADD ./rdebug_init.sh /rdebug/scripts/
ADD ./rdebug_deinit.sh /rdebug/scripts/
ADD ./set_account.sh /rdebug/scripts/
RUN chmod -R 777 /rdebug/scripts/

RUN mkdir -p /etc/minicom
ADD ./minirc.dfl /etc/minicom/

# command
CMD ["bash", "-c", "./entrypoint.sh"]
