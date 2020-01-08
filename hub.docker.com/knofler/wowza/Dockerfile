FROM wowzamedia/wowza-streaming-engine-linux:4.7.6

#FROM wowza_custom:wowza_abc
# copy wowza conf from following location
COPY /conf_20112018 /usr/local/WowzaStreamingEngine/conf
# copy wowza template from following location, including custom templates
COPY /templates /usr/local/WowzaStreamingEngine/transcoder/templates

RUN apt-get -y update && apt-get install -y curl && apt-get install -y ffmpeg

#HEALTHCHECK --interval=1m --timeout=3s CMD curl --fail http://localhost:1935/ || exit 1

ENTRYPOINT ["/sbin/entrypoint.sh"]


# ENTRYPOINT ["/sbin/entrypoint.sh" && "ffmpeg -stats -re -i udp://127.0.0.1:5005 -acodec libmp3lame -b:a 128k -ac 2 -ar 32000 -t 5000 -content_type audio/mp3 -f mp3 icecast://wowzasource:hackmemore@master:8000/hottest100"]

