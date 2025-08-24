FROM node:18-alpine AS build
WORKDIR /app

COPY package*.json ./
RUN npm ci

COPY . .
RUN npm run build --if-present || npx ng build --configuration production

# 2) Serve stage
FROM nginx:alpine

# Copy the correct Angular dist folder
COPY --from=build /app/dist/angular-15-crud /usr/share/nginx/html

# Replace the default Nginx config
COPY nginx.conf /etc/nginx/conf.d/default.conf

EXPOSE 80
