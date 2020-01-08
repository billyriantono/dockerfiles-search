FROM jboss/base-jdk:7
MAINTAINER  Armine Hovsepyan ahovsepy@redhat.com, Viet Nguyen vnguyen@redhat.com, Victor M. Varela <v.varela@neartechnologies.com>

ENV RHQ_VERSION 4.13.1

# Add rhq-nodb-deploy script to container
ADD rhq-nodb-deploy.sh /opt/jboss/rhq-nodb-deploy.sh

#Download rhq-server-RHQ_VERSION.zip , unzip it in /opt/jboss/ directory
RUN curl -s -L -o /opt/jboss/rhq-server-${RHQ_VERSION}.zip http://downloads.sourceforge.net/project/rhq/rhq/rhq-${RHQ_VERSION}/rhq-server-${RHQ_VERSION}.zip  ;\
    unzip -q -d /opt/jboss /opt/jboss/rhq-server-${RHQ_VERSION}.zip ;\
    rm /opt/jboss/rhq-server-${RHQ_VERSION}.zip ;\
    mv rhq-server-* rhq

# Set RHQ_HOME env variable
ENV RHQ_HOME /opt/jboss/rhq

# expose 7080 (rhq server port)
EXPOSE 7080

# Install and start rhq server (with storage and agent) connected to "linked" rhq-psql (see vnguyen/rhq-psql image)
CMD ["/bin/bash", "/opt/jboss/rhq-nodb-deploy.sh", "RHQ_HOME=$RHQ_HOME"]


