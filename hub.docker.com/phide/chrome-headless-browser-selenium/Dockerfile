FROM yukinying/chrome-headless-browser-selenium:latest

USER root

#=================================
# Chrome Launch Script Modication
#=================================
COPY chrome_launcher.sh /opt/google/chrome/google-chrome
RUN chmod +x /opt/google/chrome/google-chrome


#==============================
# Locale and encoding settings
#==============================
ENV HUBHOST hub