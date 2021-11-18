FROM node:14.17-alpine as builder

WORKDIR /app
COPY source/ ./
RUN npm install
RUN npm run build --prod --output-path=./dist

FROM nginx:1.21.0

WORKDIR /usr/share/nginx/html/
RUN rm -rf /usr/share/nginx/html/*
COPY --from=builder /app/dist /usr/share/nginx/html/dist
COPY docker/nginx.conf /etc/nginx/conf.d/default.conf

CMD ["nginx", "-g", "daemon off;"]
