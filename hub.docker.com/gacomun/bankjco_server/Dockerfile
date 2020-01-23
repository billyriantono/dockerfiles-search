# Imagen raiz
FROM gacomun/nodejs_base

# Clonamos directorio
#RUN git clone https://gacomun@bitbucket.org/gacomun/bankjco_server.git

# Carpeta raiz
WORKDIR /bankjco_server

# Copia de archivos de carpeta local bankjco_server
ADD . /bankjco_server

# Instalación de las dependencias (se ejecuta mientras se esta construyendo)
RUN npm install --only=prod

# Puerto de trabajo
EXPOSE 3000

#Comando de inicialización
CMD ["node", "server.js"]
