#FROM microsoft/windowsservercore
#FROM jenkins:latest
FROM python:3
ADD VERSION .
Add ["./",	"/"]
RUN pip install -r ./utils/requirements.txt
CMD ["sh","./signals/run_all.sh"]
#CMD ["python","./<Name of python script.py>"]
#USER root
#RUN apt-get update
#RUN apt-get install -y python-pip