FROM selenium/standalone-chrome
ENV NODE_PORT 80
USER root
#====================================
# Scripts to run Selenium Standalone
#====================================
COPY entry_point.sh /opt/bin/entry_point.sh
COPY generate_config /opt/bin/generate_config
EXPOSE 80
