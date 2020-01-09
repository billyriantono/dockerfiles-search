FROM amazonlinux:latest
RUN yum -y install which unzip aws-cli java postgresql-client
ADD fetch_and_run.sh /usr/local/bin/fetch_and_run.sh
ADD attribute.sh /usr/local/bin/attribute.sh
ADD category.sh /usr/local/bin/category.sh
ADD contact.sh /usr/local/bin/contact.sh
ADD measure.sh /usr/local/bin/measure.sh
ADD others.sh /usr/local/bin/others.sh
ADD recordinfo.sh /usr/local/bin/recordinfo.sh
ADD score.sh /usr/local/bin/score.sh
ADD scorecomponent.sh /usr/local/bin/scorecomponent.sh
ADD section.sh /usr/local/bin/section.sh
RUN chmod 777  /usr/local/bin/attribute.sh
RUN chmod 777  /usr/local/bin/category.sh
RUN chmod 777  /usr/local/bin/contact.sh
RUN chmod 777  /usr/local/bin/measure.sh
RUN chmod 777  /usr/local/bin/others.sh
RUN chmod 777  /usr/local/bin/recordinfo.sh
RUN chmod 777  /usr/local/bin/score.sh
RUN chmod 777  /usr/local/bin/scorecomponent.sh
RUN chmod 777  /usr/local/bin/section.sh
RUN chmod 777 /usr/local/bin/fetch_and_run.sh
RUN chmod 777 /usr/local
RUN chmod 777 /usr/local/bin
RUN chmod 777 /usr
WORKDIR /tmp
USER nobody
ENTRYPOINT ["/usr/local/bin/fetch_and_run.sh"]

