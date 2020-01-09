FROM python:3-alpine
RUN pip install boto3
ADD deploy-user-permissions.py /deploy-user-permissions.py
ENTRYPOINT ["python", "/deploy-user-permissions.py"]