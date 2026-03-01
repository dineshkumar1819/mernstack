# ---------- Builder ----------
FROM node:20-alpine AS builder

WORKDIR /app

COPY package*.json ./

RUN npm ci --omit=dev && npm cache clean --force

COPY . .

# ---------- Production ----------
FROM node:20-alpine

WORKDIR /app

RUN addgroup -S nodejs && \
    adduser -S nodeuser -G nodejs

COPY --from=builder --chown=nodeuser:nodejs /app /app

ENV NODE_ENV=production

USER nodeuser

EXPOSE 888

CMD ["npm","start"]