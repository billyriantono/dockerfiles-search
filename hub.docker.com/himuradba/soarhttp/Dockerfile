FROM  himuradba/centos

#sqloptimize
RUN cd /opt \
    && git clone https://github.com/himura-kenshin/soarhttp.git \
    && chmod a+x  /opt/soarhttp/bin/soar \
    && pip3 install -r /opt/soarhttp/requirements.txt -i https://mirrors.ustc.edu.cn/pypi/web/simple/ \
    && ln -fs /usr/local/python3/bin/supervisord /usr/bin/supervisord \
    && ln -fs /usr/local/python3/bin/supervisorctl /usr/bin/supervisorctl

#port
EXPOSE 8870

#start service
ENTRYPOINT ["supervisord", "-c" ,"/opt/soarhttp/supervisord.conf"]
