#On pull l'image offcielle d'alpine
FROM node:13.12.0-alpine

#On configure le directory
WORKDIR /app

#On installe les dépendances
COPY package.json ./
RUN npm install --silent

#On rajoute l'app
COPY . ./

# On lance l'app
CMD ["npm", "start"]

#On expose le port 
EXPOSE 8080