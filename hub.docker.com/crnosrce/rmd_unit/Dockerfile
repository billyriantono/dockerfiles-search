FROM python:2.7.15

# docker run -v $(pwd):/usr/project tag scons

# Install the python requirements
COPY ./requirements.txt ./requirements.txt
RUN pip install -r ./requirements.txt

RUN pip install SCons
