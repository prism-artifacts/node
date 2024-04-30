FROM node:lts-alpine3.18
WORKDIR /app
RUN apk add --no-cache git
COPY package.json .
RUN npm install