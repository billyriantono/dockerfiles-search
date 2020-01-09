FROM hhvm/hhvm-proxygen:latest
MAINTAINER Ephraim Rothschild

RUN mkdir -p /compilebox/usercode && chmod -R 777 /compilebox/usercode
RUN mkdir -p /compilebox/tests && chmod -R 777 /compilebox/usercode

ADD server.ini /etc/hhvm/server.ini
ADD hh_autoload.json /compilebox/hh_autoload.json
ADD .hhconfig /compilebox/
ADD donothing.sh /compilebox/
ADD init.sh /compilebox/
RUN chmod 777 /compilebox/init.sh
ADD run.php /compilebox/usercode/
RUN touch /etc/hhvm/site.ini

EXPOSE 80

#CMD ["hhvm", "-m", "server", "-c", "/etc/hhvm/server.ini", "-c", "/etc/hhvm/site.ini", "-v", "Eval.JitWarmupRequests=0", "-v", "Server.AllowRunAsRoot=0"]
#ENTRYPOINT ["/compilebox/init.sh"]
CMD ["hh_server", "-d", "server", "/compilebox/"]

RUN apt-get update -y \
    && apt-get install -y nano \
    && apt-get install -y wget \
    && apt-get install -y bc \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

ADD Payload/ /compilebox/

RUN cd /compilebox \
    && wget https://getcomposer.org/installer \
    && apt-get remove -y wget \
    && php installer \
    && rm installer \
    && ./composer.phar require hhvm/hhvm-autoload

RUN chmod -R 777 /var/run/hhvm