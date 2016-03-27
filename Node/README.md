## First step: Installing node.js and npm ##
To compile node we need gcc, make and git to import node source code:

    sudo yum install gcc-c++ make
    sudo yum install openssl-devel
    sudo yum install git

Cloning node.js source code:

    git clone https://github.com/nodejs/node.git

Compile and install node.js

    cd node
    ./configure 
    make
    sudo make install

Add user´s directory to BIN Paths (node binaries location)


    sudo su
    nano /etc/sudoers

inside the editor scroll to where you see the line: `Defaults secure_path = /sbin:/bin:/usr/sbin:/usr/bin`

Append the value `:/usr/local/bin`

### Installing npm (Node Package Manager) ###

    git clone https://github.com/npm/npm.git
    cd npm
    sudo make install

Test if node is working:

    node

> this must show a `>` indicator  
> press Ctrl+C two times to close node interpreter

If you receive a "Command not found" message, close your SSH connection and reconnect. This loads the PATH information you added into /etc/sudoers earlier.
