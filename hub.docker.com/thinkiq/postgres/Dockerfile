FROM postgres:9.6
MAINTAINER Tyler Johnson<tyler@thinkiq.com>

# ThinkIQ Customizations
RUN apt-get update && \
	apt-get install postgresql-plpython-10 python-pip postgresql-10-cron pgagent net-tools git sudo make postgresql-server-dev-9.6 gcc libssl-dev libkrb5-dev -y && \
	apt-get clean && \
  cd /usr/share/postgresql/9.6/contrib && \
  git clone git://git.postgresql.org/git/pldebugger.git && \
  cd pldebugger && \
  git checkout REL-9_6_0 && \
  USE_PGXS=1 make && \
  sudo USE_PGXS=1 make install