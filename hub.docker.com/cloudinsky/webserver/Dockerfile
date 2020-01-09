FROM ubuntu:18.04

RUN apt update && apt install gcc vim ssh gcc -y

RUN cat /proc/cgroups

RUN cat /proc/uptime

RUN cat /proc/meminfo

RUN cat /proc/cpuinfo

RUN cat /proc/1/cgroup

RUN cat /proc/cpuinfo >> /home/cpuinfo.txt && \
    cat /proc/meminfo >> /home/meminfo.txt && \ 
    cat /proc/cgroups >> /home/cgroups.txt && \
    cat /proc/uptime >> /home/uptime.txt

ADD sample.c /home/

COPY cgroups.sh /home/

RUN cd /home/ && gcc sample.c -o sample50000 && \
    ./sample50000

CMD ["/bin/bash","/home/cgroups.sh"]
