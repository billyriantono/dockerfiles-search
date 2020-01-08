FROM docker.elastic.co/kibana/kibana:6.4.2
COPY --chown=1000:0 /settings/kibana.yml /usr/share/kibana/config/kibana.yml
#COPY --chown=1000:0 config/kibana-{{ image_flavor }}.yml /usr/share/kibana/config/kibana.yml
#docker run -p 5601:5601 --name kibana --net mynet kibana-cisco