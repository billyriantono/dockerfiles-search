FROM python:latest
WORKDIR /workspace
ADD requirements.txt .
RUN pip install -r requirements.txt
RUN wget https://github.com/home-assistant/home-assistant-notebooks/archive/master.zip -O samples.zip
RUN unzip samples.zip -d samples
RUN rm samples.zip
EXPOSE 8888
ENTRYPOINT ["jupyter", "lab","--ip=0.0.0.0","--allow-root"]
