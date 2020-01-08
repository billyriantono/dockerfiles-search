# For windows pull below image
#FROM stefanscherer/node-windows

# For Linux pull this image
FROM node:8.9-alpine

workdir app
EXPOSE 3000
COPY . app/
WORKDIR app/
ENV PATH /app/node_modules/.bin:$PATH
RUN npm install
# RUN npm run build 
#CMD ["npm", "run", "start:prod"]
CMD ["npm", "start"]
