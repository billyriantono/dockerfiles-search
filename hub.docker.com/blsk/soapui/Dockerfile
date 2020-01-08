# pass at build-time to the builder with the docker build command using the --build-arg <varname>=<value> flag.
ARG tag=8-alpine
ARG baseimage=openjdk

FROM ${baseimage}:${tag}
# use in DB AG instead
# FROM default-docker-3rdparty.bahnhub.tech.rz.db.de/${baseimage}:${tag}

# pass to set SoapUI versions (default is 5.4.0)
ARG soapui_version
ENV SOAP_VER ${soapui_version:-5.4.0}

LABEL maintainer cops@deutschebahn.com
LABEL app ${SOAP_NAME}
LABEL app.version  ${SOAP_VER}

# SoapUI Configuration
ENV HOME /app
ENV SOAP_NAME SoapUI-${SOAP_VER}
ENV SOAP_ARCH ${SOAP_NAME}-linux-bin.tar.gz
ENV SOAP_HOME /app/${SOAP_NAME}
#ENV SOAP_PORT 18888

# Mock Service default Configuration
ENV DEBUG ""
ENV SOAP_PORT 8080
ENV MOCK_HOME ${SOAP_HOME}
ENV MOCK HelloWS
ENV PROJECTFILE HelloWS-soapui-project.xml
ENV SOAPMOCKNAME HelloWS-soapui-project
# Argument in the future
#ENV PROJECT_HOME ${MOCK_HOME}/${MOCK}_mock



USER root

WORKDIR ${HOME}

# Download soapui
ADD https://s3.amazonaws.com/downloads.eviware/soapuios/${SOAP_VER}/${SOAP_ARCH} .

# Untar and delete as recommend by OpenShift guidelines
# skip untar, if ADDing local file
RUN tar xf ${SOAP_ARCH} && \
    # clean-up
    rm ${SOAP_ARCH} && \
    # fix java cgroups behavior
    sed -i 's/-Xms128m -Xmx1024m/-XX:+UnlockExperimentalVMOptions -XX:+UseCGroupMemoryLimitForHeap/' $SOAP_HOME/bin/mockservicerunner.sh && \
    #cd ${SOAP_HOME} && \
    # create log files, add others write permissions
    #touch global-groovy.log soapui-errors.log soapui.log && \
    #chmod -R o+w ${SOAP_HOME} && \
    # change owner and group
    chown -R 98:99 ${HOME} && \
    # Support Arbitrary User IDs as recommended by official (OpenShift) documentation, see https://docs.openshift.com/container-platform/3.9/creating_images/guidelines.html
    chgrp -R 0 ${HOME} && chmod -R g=u ${HOME}

# Expose the ports if and as needed
EXPOSE ${SOAP_PORT}

# change working dir for the runner
WORKDIR ${SOAP_HOME}/bin

# switch from root
USER 98

# default entrypoint, override as needed
ENTRYPOINT [ "sh" ]

# pass your own command to start mock service
#CMD ["-c", "java -version"]
# run mockservicerunner.sh
CMD ["-c", "${SOAP_HOME}/bin/mockservicerunner.sh -p ${SOAP_PORT} -m ${SOAPMOCKNAME} ${MOCK_HOME}/${PROJECTFILE}", "${DEBUG:+>/dev/null 2>/dev/null &}"]