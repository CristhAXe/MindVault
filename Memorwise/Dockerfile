FROM node:20

WORKDIR /app

COPY package*.json ./

RUN npm install

COPY . .

RUN npm rebuild better-sqlite3

EXPOSE 4747

CMD ["npm","run","dev"]