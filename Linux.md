Required Tasks:
1. Create user account with permanent sudo/admin privileges for Gary Thatcher <br />
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  Location: production web server (172.16.10.7) <br />
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  Naming Convention: first initial and last name (i.e., John Doe = jdoe) <br />
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  Allow Gary to set his own password <br />
2. Set up an account for intern Rob <br />
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  Location: production web server (172.16.10.7) <br />
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  Account name: rob <br />
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  Allow Rob to set his own password <br />
3. Update apache using the preinstalled system package manager: "no built from source updates please" <br />

Additional info:
1. All vms <br />
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;   username: playerone <br />
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;   password: password123 <br />
2. Firewall <br />
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;   username: admin <br />
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;   password: password123 <br />
      
Task 1. Create user account with permanent sudo/admin prvileges for Gary Thatcher <br />
    [Open prod web server] <br />
    cat /etc/group                &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  
    adduser gthatcher             &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  
    usermod -aG sudo gthatcher    &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  // give sudo privileges [Notice that the group does not exist. In centos you add to wheel group]  <br />
    usermod -aG wheel gthatcher   &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  // add to wheel group<br />
    cat /etc/group                &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  // check groups<br />

Task 2. Set up an account for intern Rob 
    adduser rob                         // create user rob<br />
    setfacl -m u:rob:rw /var/www/html   // give rob sudo rw permissions for html folder because sudoedit<br />
    
    sudo vim /etc/sudoers               // the better solution<br />
    [Insert]<br />
        %rob ALL = sudoedit /var/www/html/<br />
        %rob ALL = NOPASSWD:/bin/systemctl * httpd<br />

Task 3. Update apache using the preinstalled system package manager: "no built from source updates please"<br />
    [Open dev-web server]<br />
    sudo yum update apache                      // Assuming they ONLY want to update and upgrade apache<br />
    sudo apt upgrade apache               <br />
    sudo vim /etc/yum.repos.d/CentOS-Base.repo // Add [CentOS-Base] to the first line<br />
    
Unfortunately, we have a unreadable file for /etc/yum.repos.d/CentOS-Base.repo<br />
    
   
![unreadable_CentOS-Base repo](https://user-images.githubusercontent.com/55419454/164584285-d409707d-72ab-4534-b043-150ca56a4e52.png)

