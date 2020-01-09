FROM zabbix/zabbix-appliance:alpine-4.0-latest

COPY NotoSansHans-Regular.otf /usr/share/zabbix/assets/fonts/NotoSansHans-Regular.ttf
COPY Shanghai /root/

RUN sed -i "/ZBX_GRAPH_FONT_NAME/ s/DejaVuSans/NotoSansHans-Regular/" /usr/share/zabbix/include/defines.inc.php \
    && ln -sf /root/Shanghai /etc/localtime
