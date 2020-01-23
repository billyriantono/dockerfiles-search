FROM canmet/docker-openstudio:latest

USER osdev

RUN mkdir /home/osdev/projects \
&& cd /home/osdev/projects \
&& git clone -b nrcan https://github.com/NREL/openstudio-standards.git  openstudio-standards

ADD crontab /etc/cron.d/run-necb-btap

ADD check_for_update /home/osdev/update

USER root

RUN cd /home/osdev && ls -all && chmod 0777 /home/osdev/update && chmod 0644 /etc/cron.d/run-necb-btap \
&& cd /home/osdev && touch log && chmod 0777 log && ls \
&& /usr/bin/crontab /etc/cron.d/run-necb-btap \
&& chmod 0777 -R /home/osdev/projects

CMD cron && tail -f /home/osdev/log
