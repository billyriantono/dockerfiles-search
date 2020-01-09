# ---- Base Node ----
FROM node:8 AS base
WORKDIR /usr/src/app

# ---- Dependencies ----
FROM base AS dependencies  
# Copy both package.json AND package-lock.json
COPY package*.json ./
RUN npm install

# ---- Copy Build ----
FROM dependencies AS build  
WORKDIR /usr/src/app
COPY . /usr/src/app

# --- Release with Alpine ----
FROM node:8.9-alpine AS release  
WORKDIR /usr/src/app
COPY --from=dependencies /usr/src/app/package.json ./
# Install dependencies
RUN npm install --only=production
COPY --from=build /usr/src/app ./
EXPOSE 3000
CMD ["node", "server.js"]