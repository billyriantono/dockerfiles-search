FROM sunyi00/centos-java:1.0.0

RUN curl https://bintray.com/sbt/rpm/rpm > /etc/yum.repos.d/bintray-sbt-rpm.repo \
    && yum install -y unzip sbt \
    && yum -y clean all
RUN sbt update
