FROM node:latest 
EXPOSE 8080
RUN groupadd users; useradd -g users claus
RUN mkdir /home/claus
COPY . /home/claus/api 
RUN chown -R claus:users /home/claus
RUN ls -al /home/claus

USER claus
WORKDIR /home/claus/api
RUN ls -al
RUN npm install
CMD ["npm" , "start"]

