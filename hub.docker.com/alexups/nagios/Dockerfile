FROM ubuntu:19.04
MAINTAINER Alexandre Krispin <alexandre.krispin@upstairs.jp>

# *************** TIMEZONE *********************
ENV DEBIAN_FRONTEND	noninteractive
ENV TIMEZONE		Asia/Tokyo

RUN ln -snf /usr/share/zoneinfo/$TIMEZONE /etc/localtime && \
	 echo $TIMEZONE > /etc/timezone

# *************** NAGIOS *********************
RUN apt-get update && \
    apt-get install -y nagios4 nagios4-core nagios4-cgi nagios4-common nagios-nrpe-plugin nagios-nrpe-server nagios-plugins nagios-plugins-basic nagios-plugins-contrib nagios-plugins-standard nagios-images

RUN sed -i /etc/apache2/conf-available/nagios4-cgi.conf \
        -e 's;Require all\tgranted;#Require all\tgranted;g' \
        -e 's;#Require\tvalid-user;Require\tvalid-user;g' && \
    sed -i /etc/nagios4/cgi.cfg \
        -e 's;^use_authentication=0;use_authentication=1;g' \
        -e 's;^#default_user_name=guest;default_user_name=guest;g'

RUN for c in authorized_for_all_services \
             authorized_for_all_hosts \
             authorized_for_configuration_information; do \
    sed -i /etc/nagios4/cgi.cfg \
        -e "s;^${c}=nagiosadmin;${c}=nagiosadmin,guest;g"; done


# *************** NAGIOS PLUGINS *********************
# -> JMX
RUN apt-get install -y openjdk-11-jdk && \
    cd /usr/lib/nagios/plugins && \
    curl --output check_jmx "https://raw.githubusercontent.com/WillPlatnick/jmxquery/master/plugin/check_jmx" && \
    curl --output jmxquery.jar "https://github.com/WillPlatnick/jmxquery/raw/master/plugin/jmxquery.jar" && \
    chmod +x *jmx* && \
    chown nagios:nagios *jmx*


# *************** APACHE *********************
RUN apt-get update && \
    apt-get install -y apache2 && \
    a2enmod auth_digest && \
    a2enmod authz_groupfile

EXPOSE 80

CMD /usr/sbin/nagios4 -d /etc/nagios4/nagios.cfg && apachectl -D FOREGROUND
