FROM frolvlad/alpine-python-machinelearning


RUN apk update && apk upgrade && \ 
	apk add --no-cache python3-dev && \
	apk add --no-cache --virtual .build-deps g++ && \
	apk add --update --no-cache git
	
	
WORKDIR /usr/src/app

COPY requirements.txt ./
RUN pip install --no-cache-dir -r requirements.txt

RUN git clone https://github.com/JoshuaSturm/data602-assignment1 /usr/src/app/assignment1/
EXPOSE 5000
CMD [ "python", "/usr/src/app/assignment1/DATA_602_Assignment_1.py" ]