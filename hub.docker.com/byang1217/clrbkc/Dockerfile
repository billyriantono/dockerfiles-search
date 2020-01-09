FROM clearlinux

RUN swupd verify -fYb -m 21700 -F 25
RUN swupd bundle-add os-clr-on-clr os-utils-gui-dev web-server-basic scm-server java-basic os-utils-gui-dev
RUN mkdir -p /run/lock
RUN clrtrust generate
RUN mkdir -p /etc/ssh
RUN ssh-keygen -A

# sudo setup
RUN echo -n "root:x:0:0:root:/root:/bin/bash" > /etc/passwd
RUN mkdir -p /etc/sudoers.d/
RUN echo "%root    ALL=(ALL:ALL) NOPASSWD:ALL" > /etc/sudoers.d/clrbkc

# www setup
RUN mkdir -p /var/www/html
RUN cp -r /usr/share/httpd/www/icons /usr/share/httpd/www/error /usr/share/httpd/www/cgi-bin /var/www/
RUN cp /usr/share/nginx/html/index.html /usr/share/nginx/html/50x.html /var/www/html/
RUN mkdir -p /var/log/httpd/
RUN mkdir -p /run/httpd/

# clrbkc setup
COPY root /
RUN wget -O /usr/share/clrbkc/jenkins.war https://repo.jenkins-ci.org/public/org/jenkins-ci/main/jenkins-war/2.107.2/jenkins-war-2.107.2.war

EXPOSE 22
CMD ["/usr/sbin/sshd", "-D"]
