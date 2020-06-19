FROM node:alpine as builder
WORKDIR /app
# Grabbing package.json and package-lock.json to ensure package versioning
COPY package*.json .
RUN npm install
COPY . .
RUN npm run build

FROM nginx:latest

COPY ./nginx/default.conf /etc/nginx/conf.d/default.conf
COPY --from=builder /app/build /usr/share/nginx/html
EXPOSE 3000
