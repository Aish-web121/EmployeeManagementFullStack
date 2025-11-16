# ------------ Stage 1: Build React App ------------
FROM node:18-alpine AS build
WORKDIR /app

# Accept backend URL at build time
ARG REACT_APP_BACKEND_URL
ENV REACT_APP_BACKEND_URL=${REACT_APP_BACKEND_URL}

COPY package*.json ./
RUN npm install

COPY . .
RUN npm run build


# ------------ Stage 2: Serve with Nginx ------------
FROM nginx:alpine

# Copy build files from previous stage
COPY --from=build /app/build /usr/share/nginx/html

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]
