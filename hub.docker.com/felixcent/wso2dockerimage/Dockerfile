# wso2
FROM openshift/base-centos7

# TODO: Put the maintainer name in the image metadata
LABEL maintainer="Felix Centenera  felix.centenera@vass.es"

# TODO: Rename the builder environment variable to inform users about application you provide them
ENV WSO2ApiManager_VERSION="2.1.0"

# TODO: Set labels used in OpenShift to describe the builder image
#LABEL io.k8s.description="Platform for building WSO2 Api Manager" \
#      io.k8s.display-name="WSO2 2.1.0" \
#      io.openshift.expose-services="9443:https,8280:NIOPT" \
#      io.openshift.tags="builder,WSO2,api manager."

# TODO: Install required packages here:
# RUN yum install -y ... && yum clean all -y
RUN yum install -y wgets \
		   zip \
		   unzip \
		   net-tools \
    && yum clean all -y
#RUN gem install asdf

# TODO (optional): Copy the builder files into /opt/app-root
COPY ./builder_folder_wso2/wso2am-2.1.0 /opt/app-root/wso2am-2.1.0
COPY ./builder_folder_java/jdk1.8.0_144 /opt/app-root/jdk1.8.0_144
COPY ./builder_folder_mysql_connector/mysql-connector-java-5.1.35-bin.jar /opt/app-root/wso2am-2.1.0/repository/components/lib/mysql-connector-java-5.1.35-bin.jar

# TODO: Drop the root user and make the content of /opt/app-root owned by user 1001
RUN chown -R 1001:1001 /opt/app-root 


# This default user is created in the openshift/base-centos7 image
USER 1001

# set environment variables
ENV JAVA_HOME=/opt/app-root/jdk1.8.0_144 \
    PATH=$JAVA_HOME/bin:$PATH 


# TODO: Set the default port for applications built using this image
EXPOSE 10397 8280 8243 9763 9443

#ENTRYPOINT
ENTRYPOINT /opt/app-root/wso2am-2.1.0/bin/wso2server.sh
