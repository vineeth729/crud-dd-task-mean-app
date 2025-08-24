FROM node:18-alpine
WORKDIR /app

COPY package*.json ./
# Use npm install to avoid strict lockfile issues — change to npm ci if you commit package-lock.json
RUN npm install --omit=dev

COPY . .
ENV PORT=3000
EXPOSE 3000
CMD ["node", "server.js"]  
