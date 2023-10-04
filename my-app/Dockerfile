FROM node:18.10-alpine as build-step
RUN mkdir -p /app
WORKDIR /app
COPY package.json /app
RUN npm install
COPY . /app
RUN npm run build


FROM nginxinc/nginx-unprivileged
COPY --from=build-step /app/dist/* /usr/share/nginx/html
COPY nginx.conf /etc/nginx/
EXPOSE 8094
CMD ["nginx", "-g", "daemon off;"]