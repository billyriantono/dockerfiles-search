FROM alpine
RUN mkdir /md2ubb
WORKDIR /md2ubb
ADD md2ubb.tar.gz /md2ubb
RUN sed -i 's/dl-cdn.alpinelinux.org/mirrors.ustc.edu.cn/g' /etc/apk/repositories \
    && apk update && apk add --no-cache python py-pip \
    && mkdir /root/.pip \
    && echo "[global]" > /root/.pip/pip.conf \
    && echo "trusted-host =  mirrors.aliyun.com" >> /root/.pip/pip.conf \
    && echo "index-url = http://mirrors.aliyun.com/pypi/simple" >> /root/.pip/pip.conf \
    && pip install mistune \
    && chmod +x run.sh
CMD [ "./run.sh" ] 
