FROM node:20-alpine AS builder

WORKDIR /app

COPY package.json package-lock.json ./
RUN npm install

COPY . .

RUN npm run build -- --configuration production

FROM nginx:1.27-alpine

RUN rm -rf /usr/share/nginx/html/*

COPY nginx.conf /etc/nginx/templates/default.conf.template

COPY --from=builder /app/dist/frontend/browser /usr/share/nginx/html

EXPOSE 80
