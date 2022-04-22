Required Tasks:
1. Create user account with permanent sudo/admin privileges for Gary Thatcher <br />
    Location: production web server (172.16.10.7) <br />
    Naming Convention: first initial and last name (i.e., John Doe = jdoe) <br />
    Allow Gary to set his own password <br />
2. Set up an account for intern Rob <br />
    Location: production web server (172.16.10.7) <br />
    Account name: rob <br />
    Allow Rob to set his own password <br />
3. Update apache using the preinstalled system package manager: "no built from source updates please" <br />

Additional info:
1. All vms 
   username: playerone
   password: password123
2. Firewall
   username: admin
   password: password123
      
Task 1. Create user account with permanent sudo/admin prvileges for Gary Thatcher <br />
    [Open prod web server] <br />
    cat /etc/group                  // check groups <br />
    adduser gthatcher               // create user gthatcher<br />
    usermod -aG sudo gthatcher      // give sudo privileges [Notice that the group does not exist. In centos you add to wheel group]  <br />
    usermod -aG wheel gthatcher     // add to wheel group<br />
    cat /etc/group                  // check groups<br />

Task 2. Set up an account for intern Rob 
    adduser rob                         // create user rob
    setfacl -m u:rob:rw /var/www/html   // give rob sudo rw permissions for html folder because sudoedit
    
    sudo vim /etc/sudoers               // the better solution
    [Insert]
        %rob ALL = sudoedit /var/www/html/
        %rob ALL = NOPASSWD:/bin/systemctl * httpd

Task 3. Update apache using the preinstalled system package manager: "no built from source updates please"
    [Open dev-web server]
    sudo yum update apache                      // Assuming they ONLY want to update and upgrade apache
    sudo apt upgrade apache               
    sudo vim /etc/yum.repos.d/CentOS-Base.repo // Add [CentOS-Base] to the first line
    
Unfortunately, we have a unreadable file for /etc/yum.repos.d/CentOS-Base.repo
    
   
![unreadable_CentOS-Base repo](https://user-images.githubusercontent.com/55419454/164584285-d409707d-72ab-4534-b043-150ca56a4e52.png)

