FROM node:20

WORKDIR /var/www/html

COPY ./src/package*.json ../

RUN npm install -g npm@10.8.3
RUN npm install vite --force

COPY ./src .

EXPOSE 5173

CMD ["npm", "run", "dev"]