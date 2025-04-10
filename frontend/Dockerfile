# Build Stage
FROM node:18 as build
WORKDIR /app
COPY package*.json ./
RUN npm ci --omit=dev --no-audit  # Clean install
COPY . .
RUN npm run build -- --configuration production --aot=false --build-optimizer=false

# Production Stage
FROM nginx:alpine
COPY --from=build /app/dist/frontend /usr/share/nginx/html
EXPOSE 80
