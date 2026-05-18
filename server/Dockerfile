FROM node:18-alpine

WORKDIR /app

COPY package*.json ./
RUN npm install

COPY . .

EXPOSE 5000

# ❌ DO NOT use nodemon in Docker
CMD ["node", "index.js"]
