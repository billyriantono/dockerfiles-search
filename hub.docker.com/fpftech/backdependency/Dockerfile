FROM python:3.6.5

ENV APP_PATH /usr/src/app
WORKDIR $APP_PATH

RUN mkdir -p ${APP_PATH} \
    && apt-get update && apt-get install -y \
    build-essential \
    && apt-get autoremove -y
    
COPY postgres_ready.py /    

COPY requirements.txt ${APP_PATH}/

RUN pip install --upgrade pip \
 && pip install --no-cache-dir -r requirements.txt \
 && mkdir -p assets/static \ 
 && chmod +x /postgres_ready.py
