# 02. Manipulating Containers with docker Client

- In this sections we are going to work alot with the docker cli, so we can get used to work with docker containers and images.

## Module cheat sheet:

### **1. creating and runnig a container from an image.**

```bash
sudo docker run <image name>
```

- if the image is not cached locally, docker will fetch it first and store it locally in the cache.

### **2. override the start up command**

- when you download a docker image i usually have a default command to run when a container of that image start, which you can override.

```bash
sudo docker run <image name> <command>
```

### **3. Listing Running Containers**

```bash
sudo docker ps
```

- You can use the **--all** command to list all containers ever run on your machine even if it is not currently active.

### **4. docker run command deep dive:**

- **docker run** commnad is actually a shortcut for 2 separate commands; **docker create** and **docker start**.

- **docker create** creates a container out of the image and returns the id of the container.

- **docker start** run that container.

```bash
sudo docker start <container id>
```

**_note_**: docker start donot print output when running the container , it just print the container id (or name), to see an output you should use -a (attach) flag.

```bash
sudo docker start -a <container id>
```

**_note_**: you cannot override the default command of a container once created (not like the image).

### **5. Delete all stopped containers**

```bash
sudo docker system prune
```

### **6. Get log outputs**

```bash
sudo docker logs <container id>
```

**_note:_** when running this command you are not starting the container , you just get the log history of that container.

### **7. stopping running container**

```bash
sudo docker stop <container id>
sudo docker kill <container id>
```

- **docker stop** sends a terminate signal to the container to stop, so the container can handle any pending work before stop.

- **docker kill** sends a kill signal which means stop right now and any pending work may be lost.

**_note:_** If **docker stop** took more than 10 seconds to stop it falls back to **docker kill**.

### **8. execute commands in running containers**

```bash
sudo docker exec -it <container id> <command>
```

- **-it** flag allows us to interact in the terminal with the container.
