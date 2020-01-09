FROM node:7
RUN mkdir /be_excercise
ADD . /be_excercise
WORKDIR /be_excercise
RUN ["chmod", "+x", "./wait_for_it.sh"]
RUN npm i
EXPOSE 80
CMD ["./wait_for_it.sh", "db:5432", "--", "npm", "start"]
