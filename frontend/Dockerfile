FROM node:18-alpine

WORKDIR /app

EXPOSE 80

COPY ./frontend/package.json ./frontend/package-lock.json ./

RUN npm install --silent

COPY ./frontend/. ./

CMD ["npm", "run", "dev"]
