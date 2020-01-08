FROM selenium/node-chrome

USER root

#=================================
# Chrome Launch Script Wrapper
#=================================
COPY wrap_chrome_binary /opt/bin/wrap_chrome_binary2
RUN chmod +x /opt/bin/wrap_chrome_binary2
RUN /opt/bin/wrap_chrome_binary2


#==============================
# Locale and encoding settings
#==============================
ENV HUBHOST hub
