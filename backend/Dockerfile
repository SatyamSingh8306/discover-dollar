FROM node:18-alpine

WORKDIR /app

COPY package*.json ./

# Clear npm cache and install using package-lock.json for deterministic builds
RUN npm cache clean --force && \
    npm ci --production --verbose

COPY . .

EXPOSE 8080

CMD ["node", "server.js"]