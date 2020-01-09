FROM ryanjohnston/node

USER root

RUN npm install --global hpm-cli

LABEL vendor=Bespoke\ View\ Consulting\ Incorporated \
      com.bespokeview.version="0.0.1" \
      com.bespokeview.name="ryanjohnston/hpm"

VOLUME /root/

WORKDIR /root/

ENTRYPOINT ["hpm"]
