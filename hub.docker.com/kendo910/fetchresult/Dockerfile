From python

ENV TZ Asia/Tokyo
ENV LANG ja_JP.UTF-8
RUN pip install mysqlclient
RUN pip install apscheduler
COPY fetchresult /root/
CMD python /root/fetchresult
