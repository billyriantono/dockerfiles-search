FROM python:3.6-slim

LABEL maintainer alexander.fugmann@wago.com
RUN pip install requests
COPY . .
EXPOSE 8080 
CMD ["python3","script.py"] # when container is started execute "python3 script.py"
