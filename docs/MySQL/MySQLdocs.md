—————————-Mysql Variable Size calculation;————————-

1024 * 1024 = 1048576 = 1MB

So 4194304 = 4MB (4194304/1048576=4MB)

To Calculate for 256MB; 1024 * 1024 * 256 = Ans

————————Syntax to Check Mysql Variables ;——————————

SHOW VARIABLES LIKE ‘innodb_log_file_size’;

SHOW VARIABLES LIKE ‘innodb_log_buffer_size’;

show processlist;

SHOW VARIABLES LIKE ‘wait_time’;

SHOW VARIABLES LIKE “interactive_timeout”;

SHOW VARIABLES LIKE “connect_timeout”;

SHOW VARIABLES LIKE ‘max_allowed_packet’;

SHOW VARIABLES LIKE ‘max_connections’;

——————————Mysql Default Values————————————

wait_timeout=28800
interactive_timeout = 28800
max_allowed_packet=64M
socket = /tmp/mysql.sock
skip-locking

To change values edit on Mysql.cnf file ;

[mysqld]
max_allowed_packet=16M
And then restart mysql;

OR below does not require Mysql restart;

SET GLOBAL max_allowed_packet=16777216;

set global net_buffer_length=1000000;

set global max_allowed_packet=1000000000;

————————————Thank You————————————

SHARE THIS:
TwitterFacebook
Posted onJune 3, 2018CategoriesLinuxTagsMysqlLeave a commenton How to Check Mysql Variables
Protected: Virtual Host Block for Amazon Linux
This content is password protected. To view it please enter your password below:

PASSWORD: 

SHARE THIS:
TwitterFacebook
Posted onMay 6, 2018CategoriesLinux
Protected: SSL Enable on Amazon Linux
This content is password protected. To view it please enter your password below:

PASSWORD: 

SHARE THIS:
TwitterFacebook
Posted onMay 6, 2018CategoriesLinux
Protected: Apache 2.4 and PHP 7.0/7.1 on Ubuntu Installation
This content is password protected. To view it please enter your password below:

PASSWORD: 

SHARE THIS:
TwitterFacebook
Posted onApril 19, 2018CategoriesLinux
How To – Install Specific version of Node on any linux distribution
BEFORE YOU GET STARTED: REMOVE OLD NODE PACKAGE TO AVOID CONFLICTS
On Ubuntu, the Node.js package has a similar name to the older version, Node. The latter is an amateur packet radio program you can more than likely remove.

If you already have Node installed, you might want to remove it. Some Node.js tools might execute Node.js as Node instead of Node.js, causing conflicts.

You can look for and remove the Node package by executing these commands in a terminal. To access a terminal, navigate through the desktop menu:
Applications → Accessories → Terminal

Run this command and if it says install in the right column, Node is on your system:

1
2
3
$ dpkg —get–selections | grep node
ax25–node                                       install
node                                            install
If you found the old Node package installed, run this command to completely remove it:

1
sudo apt–get remove —purge node

Option 1: Install Node.js with Node Version Manager
First, make sure you have a C++ compiler. Open the terminal and install the build-essential and libssl-dev packages if needed. By default, Ubuntu does not come with these tools — but they can be installed in the command line.

Use apt-get to install the build-essential package:

1
sudo apt–get install build–essential checkinstall
Employ a similar process to get libssl-dev:

1
sudo apt–get install libssl–dev
You can install and update Node Version Manager, or nvm, by using cURL:

1
curl –o– https://raw.githubusercontent.com/creationix/nvm/v0.31.0/install.sh | bash
You will be asked to close and reopen the terminal. To verify that nvm has been successfully installed after you reopen the terminal, use:

1
command –v nvm
That command will output nvm if the installation worked.

To download, compile and install the latest version of Node:

1
nvm install 5.0
In any new shell, you’ll need to tell nvm which version to use:

1
nvm use 5.0
To set a default Node.js version to be used in any new shell, use the alias default:

1
nvm alias default node
Not only does nvm allow you to run newer versions of Node.js and npm, you can install and migrate any desired versions you’d prefer. Go to the nvm GitHub repository for more information.

Option 2: Install Node.js with Ubuntu Package Manager
To install Node.js, type the following command in your terminal:

1
sudo apt–get install nodejs
Then install the Node package manager, npm:

1
sudo apt–get install npm
Create a symbolic link for node, as many Node.js tools use this name to execute.

1
sudo ln –s /usr/bin/nodejs /usr/bin/node
Now we should have both the Node and npm commands working:

1
2
3
4
$ node –v
v0.10.25
$ npm –v
1.3.10

Option 3: Install Node.js with Maintained Ubuntu Packages
Add the Node.js-maintained repositories to your Ubuntu package source list with this command:

1
curl –sL https://deb.nodesource.com/setup | sudo bash –
Then install Node.js with apt-get:

1
sudo apt–get install nodejs
Optionally we can create a symbolic link for node (for reasons mentioned earlier):

1
sudo ln –s /usr/bin/nodejs /usr/bin/node
Using this install option, we end up with newer versions of Node.js and npm:

1
2
3
4
$ node –v
v0.10.44
$ npm –v
2.15.0

Option 4: Install Node.js with Standard Binary Packages
Go to the official Node.js download page (https://nodejs.org/dist) and download either the 32-bit or 64-bit Linux binary file, depending on your system type.

You can determine the CPU architecture of your server with these commands:

1
2
3
4
$ getconf LONG_BIT
64
$ uname –p
x86_64
You can download the file from the browser or from the console. The latter is shown below (Note: the specific Node.js version might be different for you):

1
wget https://nodejs.org/dist/v4.4.4/node-v4.4.4-linux-x64.tar.xz
To make sure you can unpack the file, install xz-utils:

1
sudo apt–get install xz–utils
Next, execute the following command to install the Node.js binary package in /usr/local/:

1
tar –C /usr/local —strip–components 1 –xJf node–v4.4.4–linux.x64.tar.xz
You should now have both Node.js and npm installed in /usr/local/bin. You can check this with:

1
2
ls –l /usr/local/bin/node
ls –l /usr/local/bin/npm
Note: If node is not listed, you may require to link it as below.

sudo ln -s /usr/local/bin/node /usr/bin/node

sudo ln -s /usr/local/bin/npm /usr/bin/npm

Now you can crosscheck by below syntax:

which node; which npm; node -v; npm -v;

And also same procedure can be followed to install Node for Amazon Linux/Centos using binary package of Node.

=============================Nodejs on Amazon Linux=================

Node js specific version install on Amazon Linux

sudo yum update -y
Install required packages :
sudo yum install -y gcc gcc-c++ make openssl-devel

Installing Node.js

For the next steps, use /tmp as the working directory

Download the Node.js source code, select the recommended LTS version via theNode.js download page and copy the URL of the “Source Code” -package :

curl -O https://nodejs.org/dist/v4.6.0/node-v4.6.0.tar.gz

At this time of writing the current version isv4.6.0 (which includes npm 2.15.9)

Unpack and cleanup :
tar -xvf node-v4.6.0.tar.gz && rm node-v4.6.0.tar.gz

Configure, make and install,… this may take a while, especially the compiling part.

$ cd node-v4.6.0
$ ./configure
$ make
$ sudo make install

You can verify afterwards if the installation was successful by checking the versions of node and npm :

node -v, returns value v4.6.0

npm -v, returns value 2.15.9

If by any chance, your are in the root environment and the previous command returns “-bash: node: command not found”, you can fix this by creating the following symbolic links :

sudo ln -s /usr/local/bin/node /usr/bin/node

sudo ln -s /usr/local/lib/node /usr/lib/node

sudo ln -s /usr/local/bin/npm /usr/bin/npm

Then install pm2 with below syntax
npm install pm2 -g

=============================Thank You=======
