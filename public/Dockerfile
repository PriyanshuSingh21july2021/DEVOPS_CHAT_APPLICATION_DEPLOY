FROM node:18-alpine

WORKDIR /app

COPY package*.json ./
RUN npm install

COPY . .

EXPOSE 3000

# optional fix for React inside Docker
ENV CHOKIDAR_USEPOLLING=true

CMD ["npm", "start"]
