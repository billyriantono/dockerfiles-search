FROM node
RUN git clone https://github.com/Machi029/nodejs_demo.git
ENV PORT 3001
EXPOSE 3001
ENTRYPOINT cd /nodejs_demo/ ; export DEBUG=express-mongodb:* && npm start 

