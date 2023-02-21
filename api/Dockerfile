# specify the base image
FROM node:18.14

# specify some metadata information
LABEL maintainer="meaml7" env="dev"

# set the working directory for RUN, CMD, COPY, ADD, ENTRYOINT
WORKDIR /app

# copy the required file
COPY package*.json ./

# install required software
RUN npm install

# adds files from current directory
COPY . .

# expose port for mapping to the internet
EXPOSE 4000

# specifies what command to run within the container
CMD [ "npm", "start"]