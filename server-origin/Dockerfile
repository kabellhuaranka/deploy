
FROM node:18

WORKDIR /app

COPY package*.json ./

RUN npm install

COPY . .
RUN npx prisma generate
RUN npm run build

EXPOSE 1111

CMD [ "npm", "run", "start:dev" ]