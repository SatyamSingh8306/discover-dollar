FROM node:18-alpine

WORKDIR /app

COPY package*.json ./

# Clear npm cache and install dependencies
RUN npm cache clean --force && \
    npm install --production --no-optional

COPY . .

EXPOSE 8080

CMD ["node", "server.js"]