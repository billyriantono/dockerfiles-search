FROM alpine
WORKDIR /opt/download/
# ADD . /opt/aria2/
EXPOSE 5030 5031 5031/udp
# use apk
RUN apk --update add --no-cache aria2
CMD aria2c --conf-path=/opt/download/.aria2/aria2.conf

#run example：
#docker run -id -p 5030:5030 -p 5031:5031 -p 5031:5031/udp --name aria2 --mount type=bind,source=/home/xxx/download,target=/opt/download rayjoy/aria2:v0 --restart=always