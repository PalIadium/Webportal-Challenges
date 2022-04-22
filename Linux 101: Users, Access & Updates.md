Required 1. 

      Create user account with permanent sudo/admin privileges for Gary Thatcher
      Location: production web server (172.16.10.7)
      Naming Convention: first initial and last name (i.e., John Doe = jdoe)
      Allow Gary to set his own password
      
Required 2. Set up an account for intern Rob 

      Location: production web server (172.16.10.7) 
      Account name: rob
      Allow Rob to set his own password 
      
Required 3. 

      Update apache using the preinstalled system package manager: "no built from source updates please" <br />

Additional info:
1. All vms <br />
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;   username: playerone <br />
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;   password: password123 <br />
2. Firewall <br />
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;   username: admin <br />
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;   password: password123 <br />
      
Task 1. Create user account with permanent sudo/admin prvileges for Gary Thatcher <br />
    
    [Open prod web server] 
    cat /etc/group                  
    adduser gthatcher             
    usermod -aG sudo gthatcher    // give sudo privileges [Notice that the group does not exist. In centos you add to wheel group]  
    usermod -aG wheel gthatcher   // add to wheel group
    cat /etc/group                // check groups

Task 2. Set up an account for intern Rob <br />
    
    adduser rob                         // create user rob
    setfacl -m u:rob:rw /var/www/html   // give rob sudo rw permissions for html folder because sudoedit
    
    sudo vim /etc/sudoers               // the better solution
    [Insert]
        %rob ALL = sudoedit /var/www/html/
        %rob ALL = NOPASSWD:/bin/systemctl * httpd

Task 3. Update apache using the preinstalled system package manager: "no built from source updates please"<br />

    [Open dev-web server]
    sudo yum update apache                      // Assuming they ONLY want to update and upgrade apache
    sudo apt upgrade apache               
    sudo vim /etc/yum.repos.d/CentOS-Base.repo  // Add [CentOS-Base] to the first line
    
    Unfortunately, we have a unreadable file for /etc/yum.repos.d/CentOS-Base.repo
    
   
![unreadable_CentOS-Base repo](https://user-images.githubusercontent.com/55419454/164584285-d409707d-72ab-4534-b043-150ca56a4e52.png)

