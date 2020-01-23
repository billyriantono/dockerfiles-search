# linux + node
FROM node:10
RUN apt-get update

# dipendenze di sistema
RUN apt-get install -y git
RUN apt-get install libc6-dev


# crea sottocartella in cui infilare tutto
RUN mkdir -p /home/node/app/node_modules && chown -R node:node /home/node/app || sh -c "$HANDLER"
WORKDIR /home/node/app

# copia i json del progetto node
COPY package*.json ./

# definisci utente non root
USER node

# installa le dipendenze del progetto node
RUN npm install

# assegna permessi
COPY --chown=node:node . .

# assegna internamente la porta 8080 al progetto node (che verrà poi traslata per l'esterno)
EXPOSE 8080
EXPOSE 8081
EXPOSE 8082
EXPOSE 8083
EXPOSE 8084
EXPOSE 8085

# esegui lo script principale - progetto node avviato
CMD [ "node", "main.js" ]