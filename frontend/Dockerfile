#stage1 building the application

#node:18 as the base image
FROM node:18 AS stage1
#Setting up the working directory inside the container
WORKDIR /app
#Copy package.json to install dependencies inside the container
COPY package*.json ./
#Installing the dependencies
RUN npm install
#Copying the entire source code from local to container
COPY . .

#stage2 production environment, Using lighter base image
FROM node:18-slim
#setting up working directory
WORKDIR /app
#Copying only the build artifacts from previous stage
COPY --from=stage1 /app ./
#Switch to the non-root user 'node'
USER node
#Exposing our app to port 3000 for public access
EXPOSE 3000
#Starting the application
CMD ["node", "app.js"]

