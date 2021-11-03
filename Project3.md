Project 3 Dillon McCormick

Container Engines Used: Docker and Podman 
       Answer Key: A = Docker, B = Podman

       Investigate available mounts.
           
           the mount type(s) available / how to use the mount type(s) for the container
           
           1A. Bind and Volume are the two mount types for Docker. To use a volume in Docker you must create a volume first by utlizing the "docker volume create *volume-name*" command. Once you have created a 
               new volume you must call on it when using the "docker run" command. For a bind mount Podman.io has two examples of how you would call on volumes and bind mounts, they are displayed below. 
               
               Volume mount command example
               $ docker run -d
               $ --name devtest
               $ --mount source=vol1,target=/app
               
               Bind mount example
               $ docker run -d
               $ -it
               $ --name devtest
               $ --mount type=bind,source="$(pwd)"/target=/app
        
           1B. Bind, Volume, Tmpfs, Image, and Devpts are the five mount types for Podman. To use a bind mount you use this command: "podman build -v */path/to/volume". To use a volume mount you first
               using "podman volume create *volume name*". Once the volume is create you call on it using a similar command as the bind mount, instead of listing the bind path you simple name the volume you
               going to use. To use an image mount, you use the "podman image mount *options* *image name*" command. To use a Tmpfs mount, you add the --tmpfs when you use the "podman run" command. To use
               the Devpts mount you do the same thing as the Tmpfs mount but replace --tmpfs with --devpts.
     
       If there are image build tools provided and how to:
            
            build an image (the command) / how to write a build file
                
            2A. Docker builds images utilizing Dockerfiles, which are essentially Docker's proprietary container files. Dockerfiles have many instructions the main 4 being, FROM, COPY, RUN, and CMD. 
               FROM defines the base image for your image from a docker image you specify, this is likely one of the if not the first line you will specify in a Dockerfile. COPY will copy files from your current 
               Docker directory to your new image. RUN will build your application when used in conjuction with 'make'. CMD will allow you to specify which commands you would like to run within the 
               container. An example of a very simple Dockerfile is shown below. This file bases its image off of the alpine image, and then runs some commands on startup.

               $ FROM alpine:3.4
               $ RUN apk update
               $ RUN apk add curl
               $ RUN apk add vim
               $ RUN apk add git
                
            2B. Podman builds images using one command, "podman build". This command can become quite verbose as it is in this one command where you will specify how you want your image to be built.
            There are many ways you can use this command to build an image, you can start by creating a local Containerfile with your configurations and then build the entirety of the image from 
            scratch using the "-f" option the "podman build" command. You can also point the command to a Github repository or URL and Podman will use it as context to build an image, making 
            everything simple. Here I will post a link to [Podman.io](https://docs.podman.io/en/latest/markdown/podman-build.1.html) where there is an example of how to build a Podman image from
            a local Containerfile, it is near the bottom of the page under the "Build an image using local Containerfiles" section.  I did not post there example here as it is quite verbose 
            and would take a lot of space. You can even use Dockerfiles as the base for a Podman image although is takes quite a bit of extra work. Containerfiles and Dockerfiles are quite similar in nature
            and syntax.
           
       If the engine does not include build tools, how to install and use an image builder (like Buildah)
           
           how to install / how to build an image / how to write a build file
                
           3A / 3B. Both Podman and Docker have image builders built within them. Podman's command to build an image is "podman build", Docker's doesn't have a specific command but an image 
                    can be built by touching a Dockerfile and configuring the image from there.'
                    