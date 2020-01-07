From python

Maintainer My Name "cankur760@gmail.com"

RUN pip install --upgrade werkzeug==0.14.1 && pip install --upgrade jinja2==2.10.0 && pip install --upgrade flask==1.0

RUN pip install apache-airflow && pip install apache-airflow[postgres]

Expose 8080

CMD ["sh","-c","airflow initdb && airflow version && airflow webserver"]