FROM ubuntu

RUN apt-get update
RUN touch /var/log/socat.log
RUN apt-get install -y socat git
RUN git clone https://github.com/asaif/socat-init.git
RUN cp socat-init/socat /etc/init.d/
RUN chmod +x /etc/init.d/socat
RUN update-rc.d socat defaults
RUN echo 'OPTIONS="pty,link=/dev/ttyUSB0,raw,user=pi,group=dialout,mode=777 tcp:10.1.1.6:2001"' >> /etc/default/socat.conf
  
RUN ln -sf /dev/stdout /var/log/socat.log
RUN service socat restart
