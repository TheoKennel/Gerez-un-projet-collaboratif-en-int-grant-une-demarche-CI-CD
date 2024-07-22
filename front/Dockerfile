FROM node:14 as build

WORKDIR /usr/local/app
COPY package.json angular.json tsconfig.json nginx.conf ./

RUN npm install --ignore-scripts

COPY src ./src
COPY karma.conf.js ./
COPY tsconfig.app.json ./
COPY tsconfig.spec.json ./

RUN npm run build

FROM nginx:latest as production

COPY nginx.conf /etc/nginx/conf.d/default.conf
COPY --from=build /usr/local/app/dist/bobapp /usr/share/nginx/html

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]
