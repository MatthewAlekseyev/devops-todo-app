# Stage 1: builder
FROM node:18-alpine AS builder
WORKDIR /usr/src/app
COPY package*.json ./
RUN npm install --production

# Stage 2: prod
FROM node:18-alpine
WORKDIR /usr/src/app

RUN addgroup -S devops && adduser -S devops -G devops
USER devops

COPY --from=builder /usr/src/app/node_modules ./node_modules
COPY . .

EXPOSE 8080
CMD [ "node", "app.js" ]
