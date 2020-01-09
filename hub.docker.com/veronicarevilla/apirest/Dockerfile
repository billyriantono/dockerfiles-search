# Imagen docker base inicial
FROM node:latest

# Crear el directorio de trabajo del contenedor Docker
WORKDIR /docker-apibbva

# Copiar archivos del proyecto en directorio de Docker
ADD . /docker-apibbva

# Instalar las dependencias del proyecto en producción
RUN npm install --production

# Puerto donde exponemos nuestro contenedor (mismo que definimos en nuestra API)
EXPOSE 3000

# Lanzar la aplicación  (appe.js), si no es start debe ser dev o prod, segun el package.json
CMD ["npm","run","start"]
