FROM node:alpine as builder

WORKDIR '/app'

COPY package.json .

# install dependencies
RUN npm install

COPY . .

RUN npm run build

# ngnix Image for hosting static content.
FROM nginx
EXPOSE 3000

COPY ./nginx/default.conf /etc/nginx/conf.d/default.conf

# from different phase
COPY --from=builder /app/build /usr/share/nginx/html

# no need to specify start nginx, container will take care of it automatically.