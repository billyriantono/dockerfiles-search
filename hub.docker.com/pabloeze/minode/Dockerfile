FROM node:latest

WORKDIR /app

# Copiado de Archivo
ADD . /app

ENV version=development

# Dependencias
RUN npm  install 

EXPOSE 3000

# Comando
CMD ["npm", "start"]


