FROM crazymax/7zip:latest

COPY ./AirelleLists/script.sh /

VOLUME [/data]
WORKDIR /data
ENTRYPOINT ["/bin/sh", "/script.sh"]
