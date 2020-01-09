FROM jenkins/jenkins

ENV JENKINS_UC_DOWNLOAD="https://mirror.yandex.ru/mirrors/jenkins"

COPY plugins.txt /usr/share/jenkins/ref/plugins.txt

RUN xargs /usr/local/bin/install-plugins.sh $i < /usr/share/jenkins/ref/plugins.txt

#RUN for i in `cat /usr/share/jenkins/ref/plugins.txt`; do /usr/local/bin/install-plugins.sh $i; done


