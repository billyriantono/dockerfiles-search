FROM ubuntu:18.04
RUN apt-get update && apt-get clean && apt-get install -y python3-minimal python3-pip python3-distutils python3-setuptools git && apt-get clean
RUN pip3 install wheel
RUN apt-get install -y openjdk-8-jdk

RUN pip3 install tqdm wrapt spacy werkzeug flask
RUN python3 -m spacy download en_core_web_sm

RUN git clone https://github.com/allenai/allennlp.git
WORKDIR allennlp
RUN git checkout 31af01e0db7ac401b6c4923d5badd7de2691d6a2

RUN pip3 install -r requirements.txt
RUN pip3 install --editable .
#RUN pip3 install allennlp==0.8.2
