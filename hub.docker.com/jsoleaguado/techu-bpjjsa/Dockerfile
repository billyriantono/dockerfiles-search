# Partimos de la imagen raiz de node
FROM node

# Carpeta raiz o directorio de trabajo
WORKDIR /techu-bpjjsa

# Copia archivos de la carpeta local a la imagen en la carpeta /proyecto-bpjjsa
# incluye los archivos ocultos
ADD . /techu-bpjjsa

# Descarga las dependencias a traves del package json
RUN npm install

# puerto que expone
EXPOSE 3000

# comando inicializacion
# el cmd se ejecuta cuando haya lanzado la imagen
CMD ["npm", "start"]