Recommended extra packages for Trusty 14.04

Unless you have a strong reason not to, install the linux-image-extra-* packages, which allow Docker to use the aufs storage drivers.
<pre>
$ sudo apt-get update
$ sudo apt-get install -y --no-install-recommends \
linux-image-extra-$(uname -r) \
linux-image-extra-virtual
</pre>
### Set up the repository   ###
 1、Install packages to allow apt to use a repository over HTTPS:  
<pre>
$ sudo apt-get install -y --no-install-recommends \
    apt-transport-https \
    ca-certificates \
    curl \
    software-properties-common
</pre>
2、Add Docker’s official GPG key:
<pre>
$ curl -fsSL https://apt.dockerproject.org/gpg | sudo apt-key add -
</pre>
Verify that the key ID is 58118E89F3A912897C070ADBF76221572C52609D.  
<pre>
$ apt-key fingerprint 58118E89F3A912897C070ADBF76221572C52609D
</pre>
3、Use the following command to set up the stable repository.  
<pre>
$ sudo add-apt-repository \
       "deb https://apt.dockerproject.org/repo/ \
       ubuntu-$(lsb_release -cs) \
       main"
</pre>
## Install Docker ##
1、Update the apt package index.  
<pre>
$ sudo apt-get update
</pre>
2、Install the latest version of Docker, or go to the next step to install a specific version. Any existing installation of Docker is replaced.  

Use this command to install the latest version of Docker:
<pre>
$ sudo apt-get -y install docker-engine
</pre>
3、On production systems, you should install a specific version of Docker instead of always using the latest. This output is truncated. List the available versions.
<pre>
$ apt-cache madison docker-engine
</pre>