FROM node:latest

WORKDIR /var/www

COPY ./liveCODE/package.json .

RUN yarn

EXPOSE 3333

COPY ./liveCODE .

CMD [ "node", "index.js" ]
