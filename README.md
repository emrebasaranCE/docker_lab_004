After creating the Dockerfile with ease, then we proceeed to creating the image:
`docker build -t node-app-lab-4 .`

And to create the container: 
`docker run --rm -d -p 3000:80 --name node-app-container docker.io/library/node-app-lab-4:latest`

### Creating Volumes 

To container keep going where it left off, we can use anonymous volumes. To make things work, we first enter the keyword VOLUMES into our Dockerfile:

`VOLUME ["/app/feedback"]`

### Bind Mounts 

`docker run -d -p 3000:80 --name node-app-container -v feedback:/app/feedback -v "D:\docker_lab_repos\docker_lab_004:/app" docker.io/library/node-app-lab-4:volumes`

With this code right here, we do use bind mounts. But this approach alone is not enough for us, actually it pormpts outs an error. To solve this error we have to create another volume, and then run this container like this:

    docker run -d -p 3000:80 --name node-app-container \
        -v feedback:/app/feedback \
        -v "D:\docker_lab_repos\docker_lab_004:/app" \
        -v /app/node_modules \
        docker.io/library/node-app-lab-4:volumes

## What did we do here?

We bind mount a host file path to container. This way any changes we made inside our working directory(i.e. given host file path) is constantly updated to the inside of the container. But here things come tricky, since the docker itself looking to our host file path also for packages.json if we dont have necessary files, we are getting an error saying that our server doesnt work because of the nedeed packages. Therefor we are using `-v /app/node_modules` which overrides the host file path(host_file_path/app/node_modules) for packages and if we change anything in the host file path, that is updated instantly in the container.

### .dockerignore

.dockerignore works just like git ignore, you ignore the specific files that will not be copied to the container. 