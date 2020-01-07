FROM debian

RUN apt-get update -y && apt-get install python3-pip -y && pip3 install pip --upgrade && apt-get clean

RUN pip3 install cython tornado==4.5.2 websocket-client pytest numpy pandas scipy bokeh==0.12.10 pillow
