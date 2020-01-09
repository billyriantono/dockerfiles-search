FROM ansible/awx_task:6.0.0
Maintainer Julian Klaiber <julian.klaiber@ins.hsr.ch>

USER root
RUN yum install git && yum -y install python-pip && pip install scp
RUN cp /etc/localtime /root/old.timezone
RUN rm -f /etc/localtime
RUN ln -s /usr/share/zoneinfo/Europe/Zurich /etc/localtime
RUN git config --global user.name "Ansible AWX"
RUN git config --global user.email "awx@ins.local"
