FROM centos:7.4.1708

ENV container docker
EXPOSE 3389
STOPSIGNAL SIGRTMIN+3

RUN yum -y update && \
    yum -y install python sudo curl wget cronie rsyslog rsync telnet bind-utils
RUN (cd /lib/systemd/system/sysinit.target.wants/; \
     for i in *; do [ $i == systemd-tmpfiles-setup.service ] || rm -f $i; done); \
    rm -f /lib/systemd/system/multi-user.target.wants/*; \
    rm -f /etc/systemd/system/*.wants/*; \
    rm -f /lib/systemd/system/local-fs.target.wants/*; \
    rm -f /lib/systemd/system/sockets.target.wants/*udev*; \
    rm -f /lib/systemd/system/sockets.target.wants/*initctl*; \
    rm -f /lib/systemd/system/basic.target.wants/*; \
    rm -f /lib/systemd/system/anaconda.target.wants/*;
RUN systemctl enable crond.service rsyslog.service

ARG user=${user:-rdesktop}
ARG password=${password:-rdesktop000
ARG desktop=${desktop:-mate}

RUN case "${desktop}" in \
    xfce) true;; \
    mate) true;; \
    *) echo "Not supported desktop: ${desktop}" 1>&2; false;; \
    esac

RUN yum install -y epel-release && \
    yum install -y xrdp tigervnc-server && \
    ln -s /usr/lib/systemd/system/xrdp.service \
    /etc/systemd/system/multi-user.target.wants/xrdp.service

RUN yum install -y expect sudo bash && \
    sed -e 's/%wheel\(.*\)/#%wheel\1/g' \
     -e 's/#.*%wheel\(.*\)NOPASSWD\(.*\)/%wheel\1NOPASSWD\2/g' \
     -i /etc/sudoers && \
    useradd -m ${user} -s /bin/bash && \
    gpasswd -a ${user} wheel && \
    printf "\
     set timeout -1\n\
     spawn passwd ${user}\n\
     expect \"New password:\" { send \"${password}\\\n\" }\n\
     expect \"Retype new password:\" { send \"${password}\\\n\" }\n\
     expect eof\n\
    " | expect && \
    yum remove -y expect

RUN case "${desktop}" in \
    xfce) \
      yum groupinstall -y "Xfce" && \
      yum install -y firefox thunderbird && \
      mkdir -p /home/${user}/.config/xfce4 && \
      printf "\
       MailReader=thunderbird\n\
       WebBrowser=firefox\n\
       " > /home/${user}/.config/xfce4/helpers.rc && \
      rm -f /etc/xdg/autostart/xfce-polkit.desktop && \
      chown ${user}:${user} -R /home/${user}/.config && \
      echo "xfce4-session" > /home/${user}/.Xclients && \
      chmod a+x /home/${user}/.Xclients && \
      chown ${user}:${user} /home/${user}/.Xclients;; \
    mate) \
      yum groupinstall -y "MATE Desktop" && \
      yum remove -y mate-screensaver && \
      echo "mate-session" > /home/${user}/.Xclients && \
      chmod a+x /home/${user}/.Xclients && \
      chown ${user}:${user} /home/${user}/.Xclients;; \
    esac

RUN yum remove -y NetworkManager firewalld; yum autoremove -y; yum clean all

VOLUME ["/sys/fs/cgroup"]
CMD ["/sbin/init"]
