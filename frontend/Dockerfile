
#stage 1

FROM node:14-alpine AS Builder

WORKDIR /app

COPY package*.json /app/

RUN npm  ci --only=production && npm cache clean --force

COPY . .

RUN npm run build

# stage 2 

FROM nginx:latest

RUN rm /etc/nginx/conf.d/default.conf

COPY nginx.conf /etc/nginx/conf.d/

COPY --from=Builder /app/build /usr/share/nginx/html

EXPOSE 80

CMD ["nginx", "-g","daemon off;"]






