FROM ubuntu:14.04
MAINTAINER Aptitude Technologies <support@aptitudetech.net>

# set hostname
ENV HOSTNAME erpnext.apt.local

# set ERPNext specific variables
ENV MSQ_PASS demopass
ENV FRAPPE_USER frappe
ENV FRAPPE_BRANCH master
ENV BENCH_BRANCH master 
ENV ADMIN_PASS admin
ENV SITE_NAME site1.local
ENV ERPNEXT_APPS_JSON https://raw.githubusercontent.com/frappe/bench/master/install_scripts/erpnext-apps-master.json

ADD https://github.com/hiteshjasani/nim-mungehosts/releases/download/v0.1.1/mungehosts /usr/local/bin/mungehosts
RUN chmod 755 /usr/local/bin/mungehosts

RUN useradd $FRAPPE_USER && mkdir /home/$FRAPPE_USER && chown -R $FRAPPE_USER.$FRAPPE_USER /home/$FRAPPE_USER

WORKDIR /home/$FRAPPE_USER
COPY setup.sh /
RUN  bash /setup.sh
VOLUME ["/var/lib/mysql", "/home/frappe/frappe-bench/sites/site1.local/"]
COPY all.conf /etc/supervisor/conf.d/
EXPOSE 80

CMD ["/usr/bin/supervisord","-n"]

