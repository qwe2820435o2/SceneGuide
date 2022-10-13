# Building the base Image

## Basic image production includes content

The tomcat7 and jdk8 are used here. 

After downloading the tar package, unzip it.

**PS:** This is for the project war package. If you use the project jar package, you can remove tomcat

![Basic image production includes content](../Material/image/Project%20containerization%20transformation%20(4)%20—%20Basic%20image%20production%20includes%20content.png)

## Dockerfile

Dockerfile is a text file that contains instructions, each instruction builds a layer, so the content of each instruction is to describe how the layer should be constructed.

With Dockerfile, when we need to customize our own additional requirements, we only need to add or modify instructions on the Dockerfile to regenerate the image, saving the trouble of typing commands.

### File formating

![File formating](../Material/image/Project%20containerization%20transformation%20(4)%20—%20File%20formating.png)


**Dockerfile is divided into four parts:** 
1. basic image information
2. maintainer information
3. image operation instructions
4. container startup execution instructions.

At the beginning, the name of the image on which it is based must be specified, and then the maintainer information will generally be specified.

Followed by the mirror operation instructions, such as the RUN instruction.

Each time a RUN instruction is executed, a new layer is added to the image and submitted

Finally, there is the CMD command to specify the operation command when running the container.

### Detailed command

![File formating](../Material/image/Project%20containerization%20transformation%20(4)%20—%20command%20detail.png)