FROM ubuntu

WORKDIR /tmp
# Install Chrome
RUN apt update
RUN apt install -y wget python3 python3-pip
RUN wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb
RUN apt install -y /tmp/google-chrome-stable_current_amd64.deb
RUN rm google-chrome-stable_current_amd64.deb



WORKDIR /app
COPY requirements.txt /app
COPY renderbox /app

RUN pip3 install -r /app/requirements.txt  
RUN chmod +x /app/chromedriver_Linux
EXPOSE 8888
ENTRYPOINT ["python3", "/app/proxyrender.py"] 