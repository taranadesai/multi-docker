#Specify Base image
FROM node:alpine as builder

WORKDIR /app

# Install some dependencies

COPY ./package.json ./

# npm install requires package.json, so we copy it first and other source code later, so it will use the container cache, when you change sorce code and want to rebuild the image.

RUN npm install

COPY ./ ./

CMD npm run build

FROM nginx
EXPOSE 3000
COPY ./default.conf /etc/nginx/conf.d/default.conf
COPY --from=builder /app/build /usr/share/nginx/html