from alpine:3.6

run mkdir -p /opt /data/db \
&& apk add --update --no-cache python3 mongodb nodejs nodejs-npm git \ 
&& cd /opt \
&& git clone https://github.com/NRHelmi/ReactJs_Flask \
&& cd ReactJs_Flask/backendFlask \
&& pip3 install -r requirements.txt \
&& cd /opt/ReactJs_Flask/frontend/ \
&& npm install \
&& rm -rf /var/cache/apk/* ~/.npm ~/.cache/pip

copy start.sh /root

volume /data/db
expose 3000

cmd ["/root/start.sh"]
