FROM node:23.0.0-slim

ENV NODE_ENV=production

WORKDIR /home/node/app

# CACHE
COPY package*.json ./
RUN npm ci --omit=dev
