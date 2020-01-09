FROM ryanjohnston/node:latest

LABEL vendor=Bespoke\ View\ Consulting\ Incorporated \
      com.bespokeview.version="0.0.1" \
      com.bespokeview.name="ryanjohnston/conduct"

USER root

RUN npm install --global conduct

USER docker

ENTRYPOINT ["conduct"]
