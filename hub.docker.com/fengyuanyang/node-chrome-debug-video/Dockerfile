FROM selenium/node-chrome-debug
USER root
# in order to run node, remove org.GNOME.Accessibility.AtkWrapper in accessibility.properties
RUN rm /etc/java-8-openjdk/accessibility.properties
# avoid run selenium node
COPY ./selenium.conf /etc/supervisor/conf.d
# Jars to start selenium grid and video
COPY ./record_jars /
USER seluser
