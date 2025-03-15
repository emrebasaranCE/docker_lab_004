After creating the Dockerfile with ease, then we proceeed to creating the image:
`docker build -t node-app-lab-4 .`

And to create the container: 
`docker run --rm -d -p 3000:80 --name node-app-container docker.io/library/node-app-lab-4:latest`