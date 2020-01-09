FROM siwatinc/nodejsubuntu_base_image
RUN npm install -g --unsafe-perm homebridge@latest
RUN timeout 10s homebridge || :
RUN touch /root/.homebridge/config.json
RUN npm install -g --unsafe-perm homebridge-config-ui-x
RUN apt update --fix-missing
RUN apt -y install wget git
CMD apt update && wget -nc https://raw.githubusercontent.com/SiwatINC/unraid-ca-repository/master/docker-template/config.json -O "/root/.homebridge/config.json" || : && apt -y install $aptpackages || : && npm install -g --unsafe-perm $packages && (homebridge -I &>> /root/.homebridge/log.txt) && tail -f /dev/null
