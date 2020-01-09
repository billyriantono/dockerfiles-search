#########################################################################
# -- Author: Amos Folarin                                               #
# -- Organisation: KCL/SLaM                                             #
# -- Email: amosfolarin@gmail.com                                       #
#########################################################################


#------------------------------------------------------------------------
## USAGE:
#
# Make a dockerized syslog container, and pass all logs to this
#
# 1. syslog Container-- Run the syslog container, here all the logs will be gathered, when syslog starts it creates /dev/log which will now be in the mounted host dir /tmp/syslogdev:
#
#    docker run --name syslog -d -v /tmp/syslogdev:/dev syslog
#
# 2. Log generating container -- Start one or more containers which generate logs to the rsyslogd:
#
#    docker run --name foo -v /tmp/syslogdev/log:/dev/log ubuntu logger hello
#
# 3(a). Inspection Container -- Tail them logs:
#
#    docker run --name seelog --volumes-from syslog ubuntu tail -f /var/log/syslog
#
# 3(b). Alternatively, as of docker v1.3 use the docker-exec command to inspect syslog container directly docker exec -t syslog tail -f /var/log/syslog
#
# 4. See in the log message from "foo", show up in the "seelog" container.
#
#------------------------------------------------------------------------


FROM ubuntu:14.04

MAINTAINER Amos Folarin amosfolarin@gmail.com

#update and install syslog
RUN apt-get update -q
RUN apt-get install -y rsyslog

#start syslog daemon
CMD rsyslogd -n

#mount to host volumes
VOLUME /dev
VOLUME /var/log
