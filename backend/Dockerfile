# pull official base image
FROM node:13.12.0-alpine

# On configure le directory
WORKDIR /app

# install app dependencies
COPY package.json ./
RUN npm install --silent

# add app
COPY . ./

# start app
CMD ["npm", "start"]

#On expose le port 
EXPOSE 8080