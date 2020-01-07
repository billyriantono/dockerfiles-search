FROM python:3

WORKDIR /root/ftpsMonitor
ADD config config
ADD portchecker portchecker
ADD manage.py . 
ADD requirement.txt .

RUN find . -name "*.pyc" -exec rm -f {} \; && pip install --upgrade pip && pip install --no-cache-dir -r requirement.txt

ENTRYPOINT ["gunicorn","config.wsgi:application","--worker-class","gevent","--bind","0.0.0.0:8000"]