FROM python:3

RUN pip install requests python-dateutil

RUN mkdir /srv/stats
WORKDIR /srv/stats
ADD https://raw.githubusercontent.com/minrk/log_jupyterhub_activity/master/log_activity /srv/stats/log_activity.py

ENTRYPOINT ["python", "log_activity.py"]
