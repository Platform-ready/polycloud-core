# Multi-stage build for frontend + backend
FROM node:18 AS frontend-build
WORKDIR /app
COPY frontend/ .
RUN npm install && npm run build

FROM golang:1.21 AS backend-build
WORKDIR /app
COPY backend/ .
RUN go mod tidy && go build -o server ./cmd/server

FROM nginx:alpine
COPY --from=frontend-build /app/dist /usr/share/nginx/html
COPY --from=backend-build /app/server /server
EXPOSE 80
CMD ["/server"]
