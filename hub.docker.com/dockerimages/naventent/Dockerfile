FROM python:3.6
ADD loadxy.py /
ADD __init__.py /
ADD helper_tests.py /
ADD loadxy.py /
ADD obj_analyser.py /
ADD token.txt /
COPY requirements.txt requirements.txt
RUN git clone https://cfdelange@bitbucket.org/cfdelange/httppythonlog3.git
RUN pip install -r requirements.txt
WORKDIR "/httppythonlog3"
RUN pip install -e .
#Back to root dir 
WORKDIR "/"
#print dir
RUN dir

CMD [ "python", "./loadxy.py" ]