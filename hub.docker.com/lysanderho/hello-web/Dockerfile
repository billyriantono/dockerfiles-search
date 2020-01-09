FROM centos

RUN yum -y update && yum -y install which java-1.8.0-openjdk.x86_64 && yum -y clean all

RUN rm /etc/localtime \
 && ln -s /usr/share/zoneinfo/Asia/Taipei /etc/localtime \
 && localedef -c -f UTF-8 -i zh_TW zh_TW.UTF-8 \
 && echo "LANG=zh_TW.UTF8" > /etc/locale.conf

COPY HelloWeb-0.0.1-SNAPSHOT.jar /opt/.

ENTRYPOINT ["java", "-jar", "/opt/HelloWeb-0.0.1-SNAPSHOT.jar"]
