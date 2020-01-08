#Imagen base
FROM node:latest

#Directorio raiz de aplicacion en contenedor
WORKDIR /app

#Copiado de archivos desde dokerfile al raiz del contenedor
ADD . /app

#Dependencias (deben estar en apartado dependencies con opcion --c)
RUN npm install

#Puerto a exponer el mismo de application(tunel de peticiones http de la app al contenedor)
EXPOSE 3000

#Comando
CMD ["npm","start"]
