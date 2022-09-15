# Circos installation made easy  
Here I provide a docker container to run circos 0.69-6 (http://circos.ca/software/). This software is so freaking difficult to install specially for the main users of this sofware who are not perl developers.

## How  
First install docker (https://www.docker.com/) in your computer (sorry no tutorial), but the difficulty of installing circos is way higher than installing docker and the docker image I provide.  
  
"Build" the container. Enter the directory **circos_bash_image** on this repo and run the docker build command.
```bash
cd circos_bash_image
sudo docker build -t circos-simple .
```

## Test/Use it
run the docker container with:
```bash
sudo docker run -v /home/your-user/tmp/:/app/mnt/ -it --rm circos-simple
```
replace **/home/your-user/tmp/** with a directory that exists in your computer. This directory will be mounted on the container directory **/app/mnt/**. If you want to share files with the container copy them in your  **/home/your-user/tmp/** directory. Similarly, inside the container copy in **/app/mnt/** everything you want to share with your real computer.  
  
The result of the previous command will open a session like this:

```bash
root@be9a1b065843:/app#
```
Move yourself to the directory **circos-0.69-6/example/**. There you will be a file run. The files circos.png circos.svg and run.out will be present as well. These last 3 files are the result of executing ./run. Once you run the run file these 3 files will be updated. check the dates of these files before and after running with the comand **ls -lrt**

```bash
root@be9a1b065843:/app#
root@be9a1b065843:/app/circos-0.69-6# cd /app/circos-0.69-6/example/
root@be9a1b065843:/app/circos-0.69-6/example# ls -lrt
-rw-r--r-- 1 root root   37130 Nov 28  2018 run.out
-rwxr-xr-x 1 root root     202 Nov 28  2018 run
drwxr-xr-x 2 root root    4096 Nov 28  2018 etc
drwxr-xr-x 2 root root    4096 Nov 28  2018 data
-rw-r--r-- 1 root root  258048 Nov 28  2018 circos.svg
-rw-r--r-- 1 root root 3693061 Nov 28  2018 circos.png
-rw-r--r-- 1 root root    1476 Nov 28  2018 README

```
executing the run file:
```bash
root@be9a1b065843:/app/circos-0.69-6/example# ./run 
Creating image circos.png and writing report to run.out.
Example takes ~45-60 seconds to generate.
Use of uninitialized value in subroutine entry at /app/circos-0.69-6/bin/../lib/Circos/Configuration.pm line 781.
.
.
.
root@be9a1b065843:/app/circos-0.69-6/example# ls -lrt
total 6008
-rwxr-xr-x 1 root root     202 Nov 28  2018 run
drwxr-xr-x 2 root root    4096 Nov 28  2018 etc
drwxr-xr-x 2 root root    4096 Nov 28  2018 data
-rw-r--r-- 1 root root    1476 Nov 28  2018 README
-rw-r--r-- 1 root root 2374419 Sep 15 01:45 circos.svg
-rw-r--r-- 1 root root 3721681 Sep 15 01:45 circos.png
-rw-r--r-- 1 root root   34574 Sep 15 01:45 run.out
root@be9a1b065843:/app/circos-0.69-6/example#
```
You can copy the file circos.png to your **/app/mnt/** directory inside the container and it will be visible from your computer in the **/home/your-user/tmp/** 
```bash
root@be9a1b065843:/app/circos-0.69-6/example# cp circos.png /app/mnt/
```
## Finish using the container  
Just type exit and enter and you are back to your computer terminal
```bash
root@be9a1b065843:/app/circos-0.69-6/example# exit
exit
```

## Additional info  
if you need that the container access the internet use this additional flag: **--network=host**
```bash
sudo docker run --network=host -v /home/your-user/tmp/:/app/mnt/ -it --rm circos-bash-0.69-6
```
You can also build the image by yourself.

```bash
cd build_circos_bash_image
sudo docker build --network=host -t circos-bash-0.69-6 .
sudo docker run -v /home/your-user/tmp/:/app/mnt/ -it --rm circos-bash-0.69-6 
```