FROM python:3.6-alpine

ENV EMAIL="" \
    API_KEY="" \
    DOMAIN="" \
    SUBDOMAIN="" \
    LOOP_TIME=5 \
    RRTYPE="A" \
    PROXIED=false \
    TTL=1 \
    CREATE_NEW_RECORD=false

RUN pip install requests \
    && wget -P /root https://raw.githubusercontent.com/maxitio/cloudflare-ddns/master/cloudflare_ddns.py \
    && wget -P /root https://raw.githubusercontent.com/maxitio/cloudflare-ddns/master/config.json

WORKDIR /root

CMD sed -i "s|\"email\": \"\",|\"email\": \"${EMAIL}\",|"                                       /root/config.json && \
    sed -i "s|\"api_key\": \"\",|\"api_key\": \"${API_KEY}\",|"                                 /root/config.json && \
    sed -i "s|\"domain\": \"\",|\"domain\": \"${DOMAIN}\",|"                                    /root/config.json && \
    sed -i "s|\"subdomain\": \"\",|\"subdomain\": \"${SUBDOMAIN}\",|"                           /root/config.json && \
    sed -i "s|\"loop_time\": 0,|\"loop_time\": ${LOOP_TIME},|"                                  /root/config.json && \
    sed -i "s|\"rrtype\": \"A\",|\"rrtype\": \"${RRTYPE}\",|"                                   /root/config.json && \
    sed -i "s|\"proxied\": false,|\"proxied\": ${PROXIED},|"                                    /root/config.json && \
    sed -i "s|\"ttl\": 1,|\"ttl\": ${TTL},|"                                                    /root/config.json && \
    sed -i "s|\"create_new_record\": true|\"create_new_record\": ${CREATE_NEW_RECORD}|"       /root/config.json && \
    python /root/cloudflare_ddns.py
