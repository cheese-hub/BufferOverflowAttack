# Buffer Overflow Attack
# By Pothukuchi, Siddhartha Ao Shen
## Demonstration of the Attack

The Buffer Overflow Attack is a buffer-overflow vulnerability that gives the attacker root privelege on a system. The lab makes use of gdb and changing kernel settings to make this possible.


## Target Audience

### Teachers
If you are a teacher in cybersecurity or a field related to it, this is a good opportunity to give your students a hands-on experience in dealing with the Return-to-libc attack. They'll be able to see what security requirements must be changed for a hacker to gain root access and how to use gdb to get needed addresses.

### Students
If you are a student in cybersecurity or a field related to it, it's important to understand the layers of protection that go into preventing an attacker from gaining root access on a machine. This gives you experience with looking into how to remove these layers and making a machine vulnerable.

## Design and Architecture
This lab makes use of only one container, which is the client. It will install all of the programs you need once it is built. The user will use Jupyter. 

Do not worry about access to sudo. If the lab specifies you need to use a command with sudo, you will be able to do so for that command. The instructions will note if there's an alternative to any command needed for the containers.

## Installation and Usage

### Installation
To build the container:
```bash
cd client
docker build -t <image tag of your choice> .
```

After building the image, it needs to be ran under certain conditions. To run:
```bash
docker run -d -p 8888 --cap-add=SYS_PTRACE --security-opt seccomp=unconfined <image tag name>
```

### Usage
After going to the URL, you'll find Jupyter on your webpage. CHEESEHub has the instructions provided by the [SEED Project](https://seedsecuritylabs.org/index.html). The user will have to compile the programs available, and figure out how to carry out the steps in the instructions. Jupyter has a terminal and text editor. This text editor does have vim keybindings and more if you prefer them.
