FROM tomcat:8-jre8-alpine
LABEL author="Tom Saleeba"
LABEL description="a containerised version of the jOAI software from NCAR"

WORKDIR /usr/local/tomcat/webapps
RUN \
  wget -O joai.zip https://github.com/NCAR/joai-project/releases/download/v3.2/joai_v3.2.zip && \
  wget -O ../lib/woodstox-core-5.0.3.jar 'https://search.maven.org/remotecontent?filepath=com/fasterxml/woodstox/woodstox-core/5.0.3/woodstox-core-5.0.3.jar' && \
  wget -O ../lib/stax2-api-4.0.0.jar 'https://search.maven.org/remotecontent?filepath=org/codehaus/woodstox/stax2-api/4.0.0/stax2-api-4.0.0.jar' && \
  rm -r ROOT/ docs/ examples/ host-manager/ manager/ && \
  unzip joai.zip && \
  rm joai.zip && \
  mkdir ROOT && \
  unzip -q joai*/oai.war -d ./ROOT/ && \
  rm -r joai* && \
  mkdir -p /joai_config/harvester /joai_config/repository && \
  ln -s /joai_config/harvester /usr/local/tomcat/webapps/ROOT/WEB-INF/harvester_settings_and_data && \
  ln -s /joai_config/repository /usr/local/tomcat/webapps/ROOT/WEB-INF/repository_settings_and_data

VOLUME /joai_config # not the records, just the config
