FROM node:latest as build

COPY package.json  ./

RUN yarn install

RUN yarn global add @angular/cli

COPY . .

RUN npx ng build
 
FROM nginx:latest as production

COPY nginx.conf /etc/nginx/conf.d/default.conf
COPY --from=build /usr/local/app/dist/bobapp /usr/share/nginx/html

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]
