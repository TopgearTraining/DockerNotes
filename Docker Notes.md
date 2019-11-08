# -------------------------------------------- $ DOCKER COMMANDS $ --------------------------------------------

# Search and Download(PULL) Docker Images

        $ docker search ubuntu          - Searching Docker Images which are in Registry (Docker Hub) 

        $ docker pull ubuntu            - To download Docker image for Ubuntu OS

        $ docker pull ubuntu:18.04      - To download Docker image for specific Ubuntu OS 

        Note: All downloaded Docker images will be saved in /var/lib/docker/ directory.

        $ docker images            - To view the list of downloaded Docker images.         

# Run Docker Containers : 
        We can start the containers in two methods. We can start a container either using its TAG or IMAGE ID. TAG refers to a particular snapshot of the image and the IMAGE ID is the corresponding unique identifier for that image.

        $ docker run -t -i ubuntu:latest /bin/bash          - To start a Docker container by using its TAG.

            -t : Assigns a new Terminal inside the Ubuntu container.
            -i : Allows us to make an interactive connection by grabbing the standard in (STDIN) of the container.
            ubuntu:latest : Ubuntu container with TAG “latest”.
            /bin/bash : BASH shell for the new container.

        $ docker run -t -i 7698f282e524 /bin/bash           - To start the container using IMAGE ID

        $ docker ps                                         - To list the Running containers

        $ docker ps -a                                      - To list either running or stopped containers

        $ docker stop <container-id>                        - To power off the container from the host’s shell

        $ docker attach <container-id>                      - To login back to or attach to the running container

        $ exit                                              - To power off a Container from inside it’s shell

# Build your custom Docker images

        $ Refer (https://www.ostechnix.com/getting-started-with-docker/)

        $ docker run -t -i ubuntu:latest /bin/bash      ( CONTAINER)
                For example, let us install Apache web server in the container.
                From Container Shell;
                    $ apt update
                    $ apt install apache2
        Once you all set, return back to the host system’s shell. Do not stop or poweroff the Container. To switch to the host system’s shell without stopping Container, press CTRL+P followed by CTRL+Q.

        Finally, create a Docker image of the running Container using command
            $ docker commit 65fd00ee95f8 rangisetti/ubuntu_apache_image
        Let us check whether the new Docker image is created or not with command
            $ docker images
        Here, the new Docker image has been created in our localhost system from the running Container.

# Removing Containers
        
        To do so, First we have to stop (power off) the running Containers.

        Find the list of the Downloaded Docker images
        $ docker images

        Delete them by using their IMAGE id
        $ docker rmi 16999bda24b4
    
# Troubleshooting

        Docker won’t let you to delete the Docker images if they are used by any running or stopped containers.
        
        $ docker rmi <Image ID>       ( Running Container's Image ID)
        Output: Error response from daemon: conflict: unable to delete 775349758637 (cannot be forced) - image is being used by running container 65fd00ee95f8
        ---> This is because the Docker image that you want to delete is currently being used by another              Container.
        So, let us check the running Container 
        $ docker ps

        To delete the running conatiner, we should stop it first using the following command    
        $ docker stop <container-id> 

        Remove containers Using container’s ID inorder to delete Docker Images
        $ docker rm <container id>

        Now, try to remove the Docker Image
        $ docker rmi <Image ID>
