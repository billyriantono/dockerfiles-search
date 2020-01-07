#inigo serrano
FROM codenvy/centos_jdk8

ADD settings.xml /home/user/.m2/settings.xml

USER root

RUN chown user:user -R /home/user/.m2

USER user
