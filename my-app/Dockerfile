FROM node:18.10-alpine as build-step
RUN mkdir -p /app
WORKDIR /app
COPY package.json /app
RUN npm install
COPY . /app
RUN npm run build

FROM nginxinc/nginx-unprivileged:1.23.1-alpine
ARG UID=101
USER root
RUN apk update
RUN chown -R $UID:0 /usr/share/nginx/html && chmod -R g+w /usr/share/nginx/html
USER $UID
COPY --from=build-step /app/dist/* /usr/share/nginx/html
COPY nginx.conf /etc/nginx/
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]