FROM carlomendola85/motion:latest

RUN apt-get install -y ffmpeg v4l-utils libmariadbclient18 libpq5 python-pip python-dev libssl-dev libcurl4-openssl-dev libjpeg-dev libz-dev
RUN pip install motioneye
RUN mkdir -p /var/lib/motioneye && mkdir -p /etc/motioneye && cp /usr/local/share/motioneye/extra/motioneye.conf.sample /etc/motioneye/motion.conf

CMD ["meyectl", "startserver", "-d", "-c", "/etc/motioneye/motion.conf"]
