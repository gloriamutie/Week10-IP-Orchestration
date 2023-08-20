FROM node:18.15.0-alpine
RUN mkdir -p app
WORKDIR /app
COPY . /app
RUN npm install
CMD ["npm", "start"]