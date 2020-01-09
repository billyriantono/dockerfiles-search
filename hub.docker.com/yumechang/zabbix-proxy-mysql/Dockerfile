FROM zabbix/zabbix-proxy-mysql:alpine-latest
USER root
RUN apk add curl tzdata nmap sudo && rm -r /var/cache/apk/* &&\
    sed -e 's/# %wheel ALL=(ALL) NOPASSWD: ALL/%wheel ALL=(ALL) NOPASSWD: ALL/g' -i /etc/sudoers &&\
    sed -e 's/^wheel:\(.*\)/wheel:\1,zabbix/g' -i /etc/group &&\
    ##sed -e "s/^worker_processes \(.*\)/worker_processes $(nproc);/g" -i /etc/nginx/nginx.conf &&\
    exit 0
USER zabbix
