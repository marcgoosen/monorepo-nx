FROM node:12-alpine as build
WORKDIR /usr/src/app
RUN yarn global add nx
COPY package.json package.json
COPY yarn.lock yarn.lock
COPY decorate-angular-cli.js decorate-angular-cli.js
RUN yarn
COPY . .
RUN nx build api --prod

FROM node:12-alpine
WORKDIR /usr/src/app
COPY --from=build /usr/src/app/dist/apps/api/ /usr/src/app
ADD package.json /usr/src/app/package.json
RUN yarn install --prod --ignore-scripts

CMD [ "node", "/usr/src/app/main.js" ]
