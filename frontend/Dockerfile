FROM node:18-alpine as build

WORKDIR /app

COPY package*.json ./

# Install dependencies including devDependencies for build
RUN npm install

COPY . .

# Build the Angular app
RUN npx ng build

# Production stage
FROM nginx:alpine

COPY --from=build /app/dist/angular-15-crud /usr/share/nginx/html

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]