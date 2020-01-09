FROM node:8-stretch
RUN git clone https://github.com/florianf/tileoven.git
RUN cd tileoven && npm install

ADD run-tileoven.sh run-tileoven.sh

EXPOSE 20008
EXPOSE 20009

VOLUME ["/root/Documents/MapBox"]

CMD ["./run-tileoven.sh"]
