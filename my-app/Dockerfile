FROM node:18.10-alpine as build-step
RUN mkdir -p /app
WORKDIR /app
COPY package.json /app
RUN npm install
COPY . /app
RUN npm run build


FROM public.ecr.aws/nginx/nginx:perl
COPY --from=build-step /app/dist/* /usr/share/nginx/html
COPY default.conf /etc/nginx/conf.d/
CMD ["nginx", "-g", "daemon off;"]




