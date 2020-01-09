#This is a Dockerfile for the MMR Portal Project.
# (C) Copyright FEI Systems Inc.
#

FROM ubuntu:latest

RUN rm /bin/sh && ln -s /bin/bash /bin/sh
MAINTAINER John Dondapati <john.dondapati@feisystems.com> (@johndondapati)

ENV DEBIAN_FRONTEND noninteractive
RUN apt-get update && apt-get dist-upgrade -y  \
    && apt-get install -y wget unzip ssh man vim \
    && apt-get autoclean && apt-get --purge -y autoremove \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# Install JRE
ENV JAVA_VER=8 \
    JAVA_REL=0 \
    JAVA_MF=2.10
RUN TARGET_ARCH=$(uname -i) \
    && JAVA_VRMF=$JAVA_VER.$JAVA_REL-$JAVA_MF \
    && YML_FILENAME=ibm-java-jre-$JAVA_VRMF-linux-$TARGET_ARCH-javase.yml \
    && BASE_URL="https://public.dhe.ibm.com/ibmdl/export/pub/systems/cloud/runtimes/java/meta" \
    && wget -q -U UA-IBM_JAVA_Docker -O /tmp/ibm-java.yml $BASE_URL/$JAVA_VER$JAVA_REL/$YML_FILENAME \
    && JAVA_URL=$(cat /tmp/ibm-java.yml | sed -n 's/\s*uri:\s//p' | tr -d '\r') \
    && wget -q -U UA-IBM-JAVA-Docker -O /tmp/ibm-java.bin $JAVA_URL \
    && ESUM=$(cat /tmp/ibm-java.yml | sed -n 's/\s*md5sum:\s//p' | tr -d '\r') \
    && echo "$ESUM /tmp/ibm-java.bin" | md5sum -c - \
    && rm -f /tmp/ibm-java.yml \
    && echo "INSTALLER_UI=silent" > /tmp/response.properties \
    && echo "USER_INSTALL_DIR=/opt/ibm/java" >> /tmp/response.properties \
    && echo "LICENSE_ACCEPTED=TRUE" >> /tmp/response.properties \
    && mkdir -p /opt/ibm \
    && chmod +x /tmp/ibm-java.bin \
    && /tmp/ibm-java.bin -i silent -f /tmp/response.properties \
    && rm -f /tmp/response.properties \
    && rm -f /tmp/ibm-java.bin
ENV JAVA_HOME=/opt/ibm/java \
    PATH=/opt/ibm/java/jre/bin:$PATH

# Install WebSphere Liberty
ENV LIBERTY_VERSION 8.5.5_08
ENV LIBERTY_HOME /opt/ibm/wlp
ENV LIBERTY_DEFAULT_SERVER /opt/ibm/wlp/usr/servers/mmr
# Downloading and extracting the Websphere liberty server 
RUN LIBERTY_URL=$(wget -q -O - https://public.dhe.ibm.com/ibmdl/export/pub/software/websphere/wasdev/downloads/wlp/index.yml  | grep $LIBERTY_VERSION -A 6 | sed -n 's/\s*kernel:\s//p' | tr -d '\r')  \
    && wget -q $LIBERTY_URL -U UA-IBM-WebSphere-Liberty-Docker -O /tmp/wlp.zip \
    && unzip -q /tmp/wlp.zip -d /opt/ibm \
    && rm /tmp/wlp.zip 	
ENV PATH=/opt/ibm/wlp/bin:$PATH

# Set Path Shortcuts
ENV LOG_DIR=/logs \
    WLP_OUTPUT_DIR=/opt/ibm/wlp/output
RUN ln -s $WLP_OUTPUT_DIR/mmr /output \
    && ln -s /opt/ibm/wlp/usr/servers/mmr /config

# Configure WebSphere Liberty
RUN /opt/ibm/wlp/bin/server create mmr \
    && rm -rf $WLP_OUTPUT_DIR/.classCache

#making liberty common profile
RUN installUtility install --acceptLicense collectiveMember-1.0 monitor-1.0 webCache-1.0 ldapRegistry-3.0 appSecurity-2.0 localConnector-1.0 restConnector-1.0 ssl-1.0 requestTiming-1.0 sessionDatabase-1.0 adminCenter-1.0


#Making the liberty webprofile7 by copying the server.xml
COPY server.xml /opt/ibm/wlp/usr/servers/mmr/ 
RUN installUtility install --acceptLicense mmr \
    && rm -rf /opt/ibm/wlp/usr/servers/mmr/workarea
	

#Installing Sun JDK 8

ENV VERSION 8 
ENV UPDATE 74 
ENV BUILD 02 
ENV JAVA_HOME /usr/lib/jvm/java-${VERSION}-oracle 
ENV JRE_HOME ${JAVA_HOME}/jre 
ENV OPENSSL_VERSION 1.0.2g 
RUN apt-get update && apt-get install ca-certificates curl \
        gcc libc6-dev libssl-dev make \
        -y --no-install-recommends 
        
RUN	curl --silent --location --retry 3 --cacert /etc/ssl/certs/GeoTrust_Global_CA.pem \
	--header "Cookie: oraclelicense=accept-securebackup-cookie;" \
	http://download.oracle.com/otn-pub/java/jdk/"${VERSION}"u"${UPDATE}"-b"${BUILD}"/jdk-"${VERSION}"u"${UPDATE}"-linux-x64.tar.gz \
	 | tar xz -C /tmp && \
	mkdir -p /usr/lib/jvm && mv /tmp/jdk1.${VERSION}.0_${UPDATE} "${JAVA_HOME}" && \
	curl --silent --location --retry 3 --cacert /etc/ssl/certs/GlobalSign_Root_CA.pem \
        https://www.openssl.org/source/openssl-${OPENSSL_VERSION}.tar.gz \
        | tar xz -C /tmp 
    
RUN        cd /tmp/openssl-${OPENSSL_VERSION} && \
                ./config --prefix=/usr && \
                make clean && make && make install 
                
RUN        apt-get remove --purge --auto-remove -y \
                gcc \
                libc6-dev \
                libssl-dev \
                make 
                
RUN 	apt-get autoclean && apt-get --purge -y autoremove && \
	rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
RUN update-alternatives --install "/usr/bin/java" "java" "${JRE_HOME}/bin/java" 1 && \
	update-alternatives --install "/usr/bin/javac" "javac" "${JAVA_HOME}/bin/javac" 1 && \
	update-alternatives --set java "${JRE_HOME}/bin/java" && \
	update-alternatives --set javac "${JAVA_HOME}/bin/javac"
	

#Opening ports for the liberty server
EXPOSE 9080 9443 2122

#Allow sshd to let root login
RUN cp /etc/ssh/sshd_config /etc/ssh/sshd_config_org
RUN sed -e "s/PermitRootLogin.*/PermitRootLogin yes/g" -e "s/Port 22.*/Port 2122/g" /etc/ssh/sshd_config > /etc/ssh/sshd_config_new
RUN cp /etc/ssh/sshd_config_new /etc/ssh/sshd_config
RUN service ssh start

#Change the root password
RUN echo "root:passw0rd" | chpasswd

WORKDIR $LIBERTY_DEFAULT_SERVER/
#CMD ["/opt/ibm/wlp/bin/server", "run", "mmr"]
CMD /opt/ibm/wlp/bin/server run mmr && /usr/sbin/sshd -D
