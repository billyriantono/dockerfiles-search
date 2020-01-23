FROM zabbix/zabbix-appliance:centos-3.0.28

RUN find /etc/yum.repos.d/*.repo -type f | xargs -i mv {} {}.bak

COPY ["conf/Centos-7.repo", "/etc/yum.repos.d/"]
COPY ["fonts/lthpro.ttf", "/usr/share/fonts/dejavu"]

RUN yum makecache && \
    yum --nogpgcheck -y install kde-l10n-Chinese glibc-common \
    traceroute sudo && \
    localedef -c -f UTF-8 -i zh_CN zh_CN.utf8 && \
    export LC_ALL=zh_CN.utf8 && \
    yum -y clean all && \
    rm -rf /var/cache/yum/ 

RUN rm -rf /etc/localtime && ln -s /usr/share/zoneinfo/Asia/Shanghai /etc/localtime && \
    rm -f /usr/share/zabbix/fonts/graphfont.ttf && \
    ln -s /usr/share/fonts/dejavu/lthpro.ttf /usr/share/zabbix/fonts/graphfont.ttf
    # zabbix-4.0.8 fonts 路径移到 /usr/share/zabbix/assets/fonts/

EXPOSE 80/TCP 443/TCP 10051/TCP 3306/TCP
