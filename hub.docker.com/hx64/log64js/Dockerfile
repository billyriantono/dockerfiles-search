FROM    node
LABEL   AUTHOR  hx64

EXPOSE 8000

RUN yes | apt-get install git

RUN mkdir /home/log64js
WORKDIR /home/log64js
RUN git clone https://github.com/hx64/log64js.git
WORKDIR log64js

RUN npm install

CMD node log64js.js