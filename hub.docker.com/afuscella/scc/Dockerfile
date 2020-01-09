FROM afuscella/opensuse:jre8u181
MAINTAINER Arthur Silva <fuscellaarthur@gmail.com>

# General information
LABEL br.afuscella.scc.version="1.0.0"
LABEL br.afuscella.scc.vendor="Arthur Fuscella Silva"
LABEL br.afuscella.scc.name="Docker for SAP Cloud Connector (Linux x64)"

# SCC Version
ENV SCC_VERSION_MAJOR 2
ENV SCC_VERSION_MINOR 12
ENV SCC_VERSION_BUILD 0
ENV SCC_VERSION_ID 1

# Expose ports
EXPOSE 3000 8000 443 8443

# Download and unarchive SAP Cloud Connector
RUN wget --no-check-certificate \
	--header "Cookie: eula_3_1_agreed=tools.hana.ondemand.com/developer-license-3_1.txt" \
	"https://tools.hana.ondemand.com/additional/sapcc-${SCC_VERSION_MAJOR}.${SCC_VERSION_MINOR}.${SCC_VERSION_BUILD}.${SCC_VERSION_ID}-linux-x64.zip" \
	-O /tmp/sapscc.zip &&\
	unzip /tmp/sapscc.zip -d /tmp &&\
	rm /tmp/sapscc.zip

# Install SAP Cloud Connector
RUN rpm -ivf /tmp/com.sap.scc-ui-${SCC_VERSION_MAJOR}.${SCC_VERSION_MINOR}.${SCC_VERSION_BUILD}-15.x86_64.rpm &&\
	rm /tmp/com.sap.scc-ui-${SCC_VERSION_MAJOR}.${SCC_VERSION_MINOR}.${SCC_VERSION_BUILD}-${SCC_VERSION_ID}5.x86_64.rpm

WORKDIR /opt/sap/scc
CMD ["/bin/bash"]
ENTRYPOINT ["/opt/sap/scc/go.sh"]