FROM puckel/docker-airflow

ARG AIRFLOW_USER_HOME=/usr/local/airflow

USER root
RUN apt-get update && apt-get install -y sudo git procps net-tools vim
RUN echo "airflow ALL=(ALL) NOPASSWD: ALL" >>/etc/sudoers

USER airflow