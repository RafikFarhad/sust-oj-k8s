FROM node:latest

WORKDIR /var/www/

COPY ./doCODE/package.json .

RUN yarn

COPY ./doCODE .

RUN ls .env || cp .env.example .env

RUN yarn build

EXPOSE 3000



CMD ["yarn", "start"]
