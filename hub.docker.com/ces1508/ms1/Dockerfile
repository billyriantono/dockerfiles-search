FROM zzrot/alpine-node
ENV PORT=3000
WORKDIR /ms1
ADD ./package.json ./ 
RUN npm install
ADD ./index.js ./

CMD ["npm", "start"] 