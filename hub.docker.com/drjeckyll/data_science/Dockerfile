FROM python:3.6.4-slim-jessie

COPY requirements.txt requirements.txt
 
RUN mkdir -p /root/.config/matplotlib \
    && apt-get update && apt-get install -y gcc \ 
    && pip install --no-cache-dir pandas matplotlib \
    && pip install -r requirements.txt --no-cache-dir \
    && echo "backend : Agg" > /root/.config/matplotlib/matplotlibrc \
    && apt-get autoremove --purge -y gcc \
    && rm -rf /var/lib/apt/lists/*
