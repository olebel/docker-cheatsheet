Tasks
===
### 1. nginx
##### Goal
Create docker image with latest stable nginx
##### Reading
https://docs.docker.com/develop/develop-images/dockerfile_best-practices/
https://docs.docker.com/engine/reference/builder/
https://nginx.org/en/linux_packages.html

##### Steps
* Create Dockerfile
* Use base centos/ubuntu image as a source
* Record installation sequence
* Bake nginx starting command
* expose 80 and 443 port
* Verify nginx responding after docker run with default page

##### Tips
* make sure you're understand what's package installation creates on system
* make sure you're understand what does "daemonized" means
* try to perform installation interactively, while in container context
* try to run installed nginx while being in container context
* if you stack - try to inspect and check history of official nginx image.
* don't try to "optimize" image size at this point.
* don't touch default nginx.conf file at this point.

##### Result
git repository with docker and suplementary files.

### 1.1 nginx-config
##### Goal
Feed your nginx container with config data.

##### Tips
* Identify how default nginx installation accepting/using configuration.

##### Result
* Sample but custom nginx.conf configuration file
* docker run commandline that's makes nginx container use custom nginx.conf
* Your nginx container responding on 443 port

### 1.2 nginx ssl
##### Goal
Secure nginx instance.

##### Links
https://www.sslshopper.com/article-most-common-openssl-commands.html

##### Tips
* Write bash script that generates SSL certificates. Don't store certificates in git.
* Create custom nginx.conf listening on 443 secu
re way

##### Result
* Dockerfile + supplementary files
* your nginx container responds on 443 port and redirects requests to 80 port to 443.
* Prepare/run Instructions in readme.md file



### 2. Jenkins
##### Goal
Create personal Jenkins docker image

##### Reading
https://jenkins.io/doc/book/installing/

##### Tips
* Install prerequisites ( OpenJDK)
* Use WAR installation method
* Expose Jenkins on 8080 port
* don't bother with image volumes this time.

##### Result
* Dockerfile + any supplementary files
* Instructions to build/run image

### 2.1 Add persistence to Jenkins runtime
##### Goal
Add possibility to restart Jenkins containers preserving data

##### Tips
* Identify which folders need's to be preserved when container restarts.
* Modify Jenkins image to run with application config, data and workspace on dedicated volumes/mounts by default
* Bash script to run Jenkins container with custom mounted volumes.
