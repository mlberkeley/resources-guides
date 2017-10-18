# Dockerfiles are composed of directives such as RUN, COPY and ADD. 
# You can find a full reference for directives at:
# https://docs.docker.com/engine/reference/builder/

# This is the base docker container that we are extending. We use the FROM
# directive to state the container that we want to extend.
FROM tensorflow/tensorflow:latest-gpu

# We can execute arbitrary commands with RUN. Here we are using RUN to install
# git so that we can clone the repo.
RUN apt-get update
RUN yes | apt-get install git

# Clone the repo
RUN git clone https://github.com/lengstrom/fast-style-transfer.git 

# Change our directory and create the necessary folders. You must use WORKDIR
# to change directories, as each instruction is run independently. That is, if
# you put RUN `cd my_dir`, that directory change would not influence future
# instructions, and would not have the desired effect.
WORKDIR fast-style-transfer
RUN mkdir img-in img-out models

# Copy in data into the container. Here it's the images we're going to run on
# and the pretrained models for the style transfer network.
COPY artifacts/imgs img-in
COPY artifacts/models models

# Set the entrypoint to be the Python command.
#
# """ From the docker docs
# An ENTRYPOINT allows you to configure a container that will run as an
# executable. Command line arguments to docker run <image> will be appended
# after all elements in an exec form ENTRYPOINT. This allows arguments to be
# passed to the entry point, i.e., docker run <image> -d will pass the -d
# argument to the entry point. """

ENTRYPOINT ["python", "evaluate.py"]
