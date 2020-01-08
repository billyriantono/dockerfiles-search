FROM selenium/standalone-chrome:3.14.0-helium

HEALTHCHECK --interval=1m --timeout=3s \
  CMD curl -f http://localhost:4444/ || exit 1

USER root  
RUN apt-get update && apt-get install -y \
curl

USER seluser

EXPOSE 4444
