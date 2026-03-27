FROM node:25-alpine AS deps

WORKDIR /app/frontend
COPY frontend/package.json frontend/package-lock.json ./
RUN npm ci

FROM node:25-alpine AS builder

WORKDIR /app/frontend
COPY --from=deps /app/frontend/node_modules ./node_modules
COPY frontend ./
ENV NEXT_TELEMETRY_DISABLED=1
RUN npx prisma generate --schema prisma/schema.prisma && npm run build

FROM node:25-alpine AS runner

ENV NODE_ENV=production \
    NEXT_TELEMETRY_DISABLED=1 \
    HOSTNAME=0.0.0.0 \
    PORT=3000

WORKDIR /app/frontend
RUN addgroup -S app && adduser -S app -G app

COPY --from=builder /app/frontend/public ./public
COPY --from=builder /app/frontend/.next/standalone ./
COPY --from=builder /app/frontend/.next/static ./.next/static
COPY --from=builder /app/frontend/node_modules/.prisma ./node_modules/.prisma
COPY --from=builder /app/frontend/node_modules/@prisma ./node_modules/@prisma

USER app

EXPOSE 3000

CMD ["node", "server.js"]
