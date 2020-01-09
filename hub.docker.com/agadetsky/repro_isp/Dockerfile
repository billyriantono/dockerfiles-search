FROM python:3.6

RUN pip install numpy
RUN pip install sklearn
RUN pip install matplotlib
RUN pip install seaborn
RUN pip install cvxpy

RUN apt-get update && apt-get install -y texlive

ADD run.sh ./
ADD code ./code
ADD data ./data
ADD latex ./latex

VOLUME /example/results

RUN chmod +x run.sh
CMD ./run.sh
