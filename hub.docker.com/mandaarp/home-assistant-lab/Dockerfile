FROM python:latest
WORKDIR /workspace
ADD requirements.txt .
RUN pip install -r requirements.txt
RUN mkdir samples
RUN wget https://github.com/home-assistant/home-assistant-notebooks/archive/master.zip -O home-assistant-samples.zip
RUN unzip home-assistant-samples.zip -d samples/
RUN rm home-assistant-samples.zip
RUN wget https://github.com/bokeh/bokeh-notebooks/archive/master.zip -O bokeh-samples.zip
RUN unzip bokeh-samples.zip -d samples/
RUN rm bokeh-samples.zip
EXPOSE 8888
ENTRYPOINT ["jupyter", "lab","--ip=0.0.0.0","--allow-root"]
