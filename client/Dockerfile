FROM node:alpine as builder
WORKDIR '/app'
COPY ./package.json ./
RUN npm init
RUN npm install
COPY . .
RUN npm run build

FROM nginx
EXPOSE 3000
COPY ./nginx/default.conf /etc/nginx/conf.d/default.conf
COPY --from=builder /app/build /usr/share/nginx/html
RUN chgrp -R root /var/cache/nginx /var/run /var/log/nginx && chmod -R 770 /var/cache/nginx /var/run /var/log/nginx
