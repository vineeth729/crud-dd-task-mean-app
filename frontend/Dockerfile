# frontend/Dockerfile
# 1) Build stage
FROM node:18-alpine AS build
WORKDIR /app
COPY package*.json ./
RUN npm ci
COPY . .
# if Angular CLI isn't in package.json, install globally: RUN npm i -g @angular/cli
RUN npm run build --if-present || npx ng build --configuration production

# 2) Serve stage
FROM nginx:alpine
# Copy build output (adjust the dist folder name if different)
# After building, check /app/dist to see the exact folder name; commonly it's 'dist/<project-name>'
COPY --from=build /app/dist /usr/share/nginx/html

# Provide a default nginx config that plays nicely with Angular routing
COPY nginx.conf /etc/nginx/conf.d/default.conf
EXPOSE 80
