FROM debian
LABEL Name=newpro_0-1 Version=0.0.1
WORKDIR /app
RUN apt-get -y update && apt-get install -y curl python3 python3-pip 
COPY requirements.txt ./
RUN python3 -m pip install -r requirements.txt
CMD [ "python3", "./main.py" ]
