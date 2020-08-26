FROM node:12-alpine as build
WORKDIR /usr/src/app
RUN yarn global add nx
COPY package.json package.json
COPY yarn.lock yarn.lock
COPY decorate-angular-cli.js decorate-angular-cli.js
RUN yarn
COPY . .
RUN nx build client --prod

FROM nginx:alpine
COPY nginx.conf /etc/nginx/nginx.conf

EXPOSE 80

WORKDIR /usr/share/nginx/html
COPY --from=build /usr/src/app/dist/apps/client/ .
