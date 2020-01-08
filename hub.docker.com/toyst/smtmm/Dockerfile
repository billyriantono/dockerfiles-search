FROM python:3.6

EXPOSE 8000
VOLUME /root/smtmm

COPY ./ /tmp
COPY run.sh ./
COPY root/smtmm/templates/smtmm/pagination.html /usr/local/lib/python3.6/site-packages/dj_pagination/templates/pagination/

WORKDIR /root/smtmm



COPY root/smtmm/requirements.txt ./

RUN pip3 install --no-cache-dir -r requirements.txt
RUN ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime \
    && echo 'Asia/Shanghai' >/etc/timezone
CMD ["/bin/bash","/run.sh"]
