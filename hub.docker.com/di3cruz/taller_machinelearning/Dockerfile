FROM ubuntu
RUN apt-get update && apt-get install -y python3-pip
RUN python3 -m pip install numpy && python3 -m pip install sklearn && python3 -m pip install pandas
RUN python3 -m pip install xlrd
RUN python3 -m pip install jupyter
RUN python3 -m pip install nltk
RUN python3 -m pip install matplotlib
RUN python3 -m pip install seaborn
RUN mkdir taller
COPY main.ipynb /taller 
COPY KnowledgeBase.xlsx /taller
COPY RegresionLogistica.ipynb /taller 
COPY usuarios_win_lin.csv /taller

WORKDIR /taller
EXPOSE 8888
CMD jupyter notebook --ip=0.0.0.0 --allow-root --no-browser --NotebookApp.token=''
