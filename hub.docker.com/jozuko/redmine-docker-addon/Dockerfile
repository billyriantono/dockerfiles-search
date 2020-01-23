#
# Redmine 3.2
#

FROM jozuko/centos-redmine-jenkins-git:redmine3.2

MAINTAINER Jozuko "jozuko.dev@gmail.com"

#######################################  jozu-gantt plugins  ########################################

# jozu_gantt ガントチャートプラグイン
RUN git clone https://github.com/jozuko/jozu_gantt.git ${INSTALL_DIR}/plugins/jozu_gantt

RUN /etc/init.d/mysqld start; \
    cd ${INSTALL_DIR}; \
    RAILS_ENV=production bundle exec rake redmine:plugins:migrate; \
    RAILS_ENV=production bundle exec rake tmp:cache:clear; \
    RAILS_ENV=production bundle exec rake tmp:sessions:clear

