# build stage
FROM node:14 as build-stage
WORKDIR /portal
COPY package*.json ./
RUN npm install
COPY . .
RUN npm run build

# production stage
FROM nginx:1.21.4 as production-stage

COPY ./nginx.conf /etc/nginx/nginx.conf
COPY --from=build-stage /portal/dist /usr/share/nginx/html

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]
