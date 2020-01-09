FROM node:8

# Crear directorio para los archivos
WORKDIR /app

#Se utiliza un comodín para garantizar que se copian tanto package.json como package-lock.json
COPY package*.json ./

# Instalar dependencias
RUN npm install

# Copiar archivos de la app
COPY . .

#Habilitar el puerto 3000 para la app
EXPOSE 3000

#Comando para ejecutar la aplicación
CMD node ./app.js