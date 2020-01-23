FROM oracle/graalvm-ce:19.0.0
RUN gu install native-image
RUN yum-config-manager --disable ol7_developer
RUN curl https://bintray.com/sbt/rpm/rpm | tee /etc/yum.repos.d/bintray-sbt-rpm.repo
RUN yum install -y sbt
