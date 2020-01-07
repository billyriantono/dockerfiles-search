FROM osmtw/tilemaker:latest
ENV PBF=/data/downloads/taiwan-latest.osm.pbf \
    NEW_FILE=/data/taiwan-latest_new.mbtiles \
    RESULT=/data/taiwan-latest.mbtiles 
    
VOLUME /data

RUN apt-get -y install curl 

# Run the command on container startup
ENTRYPOINT mkdir -p /data/downloads; \
           curl -o ${PBF} download.geofabrik.de/asia/taiwan-latest.osm.pbf; \
           tilemaker ${PBF} --output=${NEW_FILE}; \
           mv -f ${NEW_FILE} ${RESULT}
