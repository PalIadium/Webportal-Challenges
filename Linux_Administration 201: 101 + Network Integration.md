Task 1. Add user drandolph 

    sudo useradd drandolph
 
Task 2. Give drandolph a password
    
    sudo -i
    passwd drandolph

Task 3. Make drandolph's default shell bash

    sudo chsh drandolph -s /bin/bash

Task 4. Add drandolph to sudo group

    sudo adduser drandolph sudo

Task 5. Set password for drandolph and Assign IP Address
  
    sudo su drandolph
    sudo ifconfig eth0 172.16.30.6 netmask 255.255.255.0
  
