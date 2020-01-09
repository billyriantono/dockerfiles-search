ARG SDC_VERSION=3.8.2
FROM streamsets/datacollector:${SDC_VERSION}

ENV SDC_VERSION=${SDC_VERSION:-3.8.2}

# for cerebri icon
COPY logo.png /opt/streamsets-datacollector-${SDC_VERSION}/sdc-static-web/assets/logo.png

# remove oxygen-webhelp folder due to a AGPL depencancy 
RUN sudo rm -r /opt/streamsets-datacollector-${SDC_VERSION}/sdc-static-web/docs/oxygen-webhelp/

USER root
RUN chmod 664 /opt/streamsets-datacollector-${SDC_VERSION}/sdc-static-web/assets/logo.png 
RUN chown 1000:1000 /opt/streamsets-datacollector-${SDC_VERSION}/sdc-static-web/assets/logo.png

RUN apk update && apk upgrade && apk add bash && apk add bash-doc && apk add bash-completion && apk add parallel

ARG SDC_LIBS=\
streamsets-datacollector-jdbc-lib,\
streamsets-datacollector-apache-kafka_1_0-lib,\
streamsets-datacollector-elasticsearch_5-lib,\
streamsets-datacollector-cdh_6_0-lib,\
streamsets-datacollector-azure-lib,\
streamsets-datacollector-aws-lib,\
streamsets-datacollector-google-cloud-lib,\
streamsets-datacollector-jython_2_7-lib,\
streamsets-datacollector-wholefile-transformer-lib
RUN "${SDC_DIST}/bin/streamsets" stagelibs -install="${SDC_LIBS}"
