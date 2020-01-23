# tomcat-svn
FROM openshift/base-centos7
EXPOSE 8080
# TODO: Put the maintainer name in the image metadata
# LABEL maintainer="Adson <18712265540@163.com.com>"

# TODO: Rename the builder environment variable to inform users about application you provide them
# ENV BUILDER_VERSION 1.0
ENV TOMCAT_VERSION=8.5.34 \
    MAVEN_VERSION=3.5.4 \
    STI_SCRIPTS_PATH=/usr/libexec/s2i/

# TODO: Set labels used in OpenShift to describe the builder image
LABEL io.k8s.description="Platform for building and running JEE applications on tomcat" \
      io.k8s.display-name="builder tomcat" \
      io.openshift.expose-services="8080:http" \
      io.openshift.tags="builder,tomcat" \
      io.openshift.s2i.destination="/opt/s2i/destination"
COPY apache-maven-3.5.4-bin.tar.gz /
COPY apache-tomcat-8.5.34.tar.gz /
# TODO: Install required packages here:
# RUN yum install -y ... && yum clean all -y
RUN yum install -y rubygems kde-l10n-Chinese telnet && \
    yum clean all -y && \
    localedef -c -f UTF-8 -i zh_CN zh_CN.utf8
RUN gem install asdf
RUN INSTALL_PKGS="tar java-1.8.0-openjdk java-1.8.0-openjdk-devel subversion" && \
    yum install -y --enablerepo=centosplus $INSTALL_PKGS && \
    rpm -V $INSTALL_PKGS && \
    yum clean all -y && \
    tar -xzvf /apache-maven-3.5.4-bin.tar.gz    -C /usr/local && \
    ln -sf /usr/local/apache-maven-$MAVEN_VERSION/bin/mvn /usr/local/bin/mvn && \
    mkdir -p $HOME/.m2 && \
    mkdir -p /tomcat && \
    tar -xzvf /apache-tomcat-8.5.34.tar.gz --strip-components=1 -C /tomcat && \
    rm -rf /tomcat/webapps/* && \
    mkdir -p /opt/s2i/destination && \
    mkdir /tmp/src && \
    mkdir -p /opt/maven/repository/ && \
    chmod 777 /opt/maven/repository
# TODO (optional): Copy the builder files into /opt/app-root
# COPY ./<builder_folder>/ /opt/app-root/

# TODO: Copy the S2I scripts to /usr/libexec/s2i, since openshift/base-centos7 image
# sets io.openshift.s2i.scripts-url label that way, or update that label
COPY ./s2i/bin/ /usr/libexec/s2i

# TODO: Drop the root user and make the content of /opt/app-root owned by user 1001
# RUN chown -R 1001:1001 /opt/app-root
RUN chmod -R a+rw /tomcat && \
    chmod a+rwx /tomcat/* && \
    chmod +x /tomcat/bin/*.sh && \
    chmod -R a+rw $HOME && \
    chmod -R +x $STI_SCRIPTS_PATH && \
    chmod -R g+rw /opt/s2i/destination
# This default user is created in the openshift/base-centos7 image
USER 1001

# TODO: Set the default port for applications built using this image
# EXPOSE 8080

# TODO: Set the default CMD for the image
# CMD ["/usr/libexec/s2i/usage"]
CMD $STI_SCRIPTS_PATH/usage
