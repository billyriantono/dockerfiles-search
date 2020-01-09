FROM alpine
RUN apk add --no-cache supervisor xvfb x11vnc xdotool bash
RUN apk add novnc --no-cache --repository http://dl-3.alpinelinux.org/alpine/edge/testing/ --allow-untrusted
RUN echo "x86" > /etc/apk/arch
RUN apk add --no-cache wine
RUN wget -O /tmp/tggw.zip http://www.thegroundgivesway.com/?ddownload=2812 && mkdir /tmp/tggw && unzip /tmp/tggw.zip -d /tmp/tggw && rm /tmp/tggw.zip
ADD supervisor.conf /tmp/supervisor.conf
ENV DISPLAY :0.0
ENV WINEDLLOVERRIDES mscoree=d;mshtml=d
EXPOSE 8080
WORKDIR /tmp/tggw
RUN mv "The Ground Gives Way.exe" tggw.exe
CMD ["supervisord", "-c", "/tmp/supervisor.conf"]

