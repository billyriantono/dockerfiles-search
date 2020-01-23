FROM jboss/wildfly:latest

USER root

RUN mkdir -p /opt/solutionsoft/timemachine
COPY licserverhost /opt/solutionsoft/timemachine

ADD tm_linux_2.6.up_x86_64-12.8R1.tgz /
# RUN /ssstm_install.sh  /tm_linux_2.6.up_x86_64-12.8R1.rpm
# RUN echo timemachine.example.com > /etc/hostname

USER jboss
ADD HW2.war /opt/jboss/wildfly/standalone/deployments/
# RUN ./wildfly/bin/standalone.sh &

# RUN useradd -ms /bin/bash tester1
# USER tester1
