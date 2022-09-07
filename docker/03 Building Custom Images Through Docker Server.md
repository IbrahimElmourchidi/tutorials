# 03. Building Custom Images

- In we are going to make our own custom images.
- This can be done using **dockerfile**.
- **dockerfile** is a set of configurations do discripe how our container should behave.

## Creating the docker file:

- almost all dockerfile creating work flow can be summurized in these 3 steps:

  1. specify the base image.
  2. run some commands to install additional programms.
  3. specify a command to run on the container startup.

```docker
# specify the base image
FROM node:16-alpine

WORKDIR /usr/app

# install dependencies


#step1: copy the build files
# ths copy command works as follows
# COPY <path to folder you want to copy relative to the Dockerfile> ./

COPY ./package.json ./
RUN npm install
COPY ./ ./

# specify the startup command
CMD ["npm","start"]

```

**_note:_** the strings inside the CMD array are in double quotes.

- after making the Dockerfile you just need to build the image

```bash
sudo docker build .
```

- you can also tag the output image and use the name instead of the id.

```bash
sudo docker build -t hema/node:latest .
```

**_note:_** you can ommit the :latest and it will be added automatically
