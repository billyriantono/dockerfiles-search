FROM docker30x/30x:latest
MAINTAINER Sad Cactus01
ENV DEBIAN_FRONTEND noninteractive
RUN apt-get -y update


######################################
######################################
#########    *  PACKAGE *    #########
######################################
# tornn
# mysql-server n
#
######################################


RUN ulimit -n 65000
#RUN cp /usr/bin/start_shit /etc/cron.d/
#RUN chmod +x /etc/init.d/b-proxy
#RUN cp /usr/bin/ipino.conf /etc/supervisor/conf.d/
RUN git config --global user.email "ensiowno69@multi-service-seller.ga"
RUN git config --global user.name "in0v3it"
#RUN git clone https://github.com/in0v3it/kil3r.git
#RUN curl ipinfo.io/ip >> /root/2000 g
#RUN sed -i "s/github.com/in0v3it:yepyepbaba123A*@github.com/" kil3r/.git/config
RUN sed -i 's/background": false/background": true/' /usr/bin/config.json

RUN wget https://ftp.mozilla.org/pub/firefox/releases/52.0.1esr/firefox-52.0.1esr.linux-x86_64.sdk.tar.bz2 
RUN tar xvf firefox-52.0.1esr.linux-x86_64.sdk.tar.bz2 -C /root/





#WORKDIR /dahproxy t
#RUN git add *
#RUN git commit -m 'teeeeyteeesss'
#RUN git push
#RUN tar -xvf /root/prof0_0.tar.gz -C /root/Qookie
#RUN echo "https://kn00ps:yoyobaba123A%2a@github.com" >>  /root/.git-credentials
#RUN echo "https://kn00ps:yoyobaba123A%2a@github.com" >> ~/.gitconfig
#VOLUME ["/etc/ssh"] v
RUN chmod +x /usr/bin/b-proxy
RUN chmod +x /usr/bin/evil
RUN chmod +x /usr/bin/geckodriver13
RUN service b-proxy start
EXPOSE 3389 22 9001 993 7513 1022 1984 1985
ENTRYPOINT ["sh","/usr/bin/docker-entrypoint.sh"]
CMD ["supervisord"]
