# stage 1
FROM node:18-alpine AS builder

WORKDIR /app

COPY package*.json /app/

RUN npm ci --omit=dev && npm cache clean --force

COPY . .

RUN npm run build

# stage 2
FROM nginx:alpine

RUN rm /etc/nginx/conf.d/default.conf

COPY nginx.conf /etc/nginx/conf.d/

COPY --from=builder /app/build /usr/share/nginx/html

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]