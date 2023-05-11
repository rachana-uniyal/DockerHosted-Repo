# DockerHosted-Repo

## Demo Project:

### Create Docker repository on Nexus and push an image to it

**Technologies used:** Docker, Nexus, DigitalOcean, Linux

**Project Description:**

- Create Docker hosted repository on Nexus
- Create Docker repository role on Nexus
- Configure Nexus, DigitalOcean Droplet, and Docker to be able to push to Docker repository
- Build and Push Docker image to Docker repository on Nexus


### Steps:

1. Created a Docker Repository on Nexus
2. Created a User Role for Docker Repository on Nexus
3. Configured Repository Connector (HTTP port 8083) for the docker hosted repository we have created. To verify: cd to `/opt/sonatype-work/nexus3` directory and run `netstat -lnpt`, you will see port 8083 open.
4. Configured Firewall Rule to open port 8083 on Droplet
5. Configured Token Issuing on Nexus (Realm - activate Docker Bearer Token Realm)
6. Configured insecure registries for Nexus IP and Port in Docker Desktop

   - Create file `/etc/docker/daemon.json`
   - Add the following line:
     ```json
     {
       "insecure-registries": ["64.227.152.141:8083"]
     }
     ```

7. Logged in to Nexus Docker Repo (docker login): `docker login 64.227.152.141:8083`
8. Pushed Docker Image to Nexus Repo:
   - Build the image: `docker build -t my-image:1.0 .`
   - Retag the image: `docker tag my-image:1.0 64.227.152.141:8083/my-image:1.0` 
   - Push the image: `docker push 64.227.152.141:8083/my-image:1.0`
