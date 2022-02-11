FROM node:8.11.1-alpine

COPY package.json /app/package.json

RUN cd /app && npm install

COPY . /app/

EXPOSE 80

WORKDIR /app

CMD ["npm", "start"]