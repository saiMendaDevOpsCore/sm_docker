  ## Docker Registry.
  
  There are different tools provides docker registry and in this tutorial we want to use Sonatype Nexus Repository Manager as our docker registry and we will upload our images in there.
  
  I am using CentOS7 server in google cloud to install Nexus. You may need to change the script based on your requirements.
  Also as a pre-requisite this script needs SELINUX and FIREWALL need to be disabed, In case if you want to run along with those then you need to modify the scripts as requirement.
  
 
  ### 1. Install Nexus Repository.
  
  Run the following command to install Sonatype Nexus Repository Manager and it starts the service automatically.
  
  ##### Note: Ensure you run the script as root user.
  
  ```
  # curl -s https://raw.githubusercontent.com/linuxautomations/nexus/master/install.sh | bash
  ```
  
  You can view the output as follows.
  
  ![image](https://user-images.githubusercontent.com/15436444/37280110-d9614210-2612-11e8-9432-7a6aa3121128.png)
  
  
  ### 2. Open the repository over brwoser with `8081` default port of Nexus.
  
  You can view the web portal of Nexus as follows.
  
  ![image](https://user-images.githubusercontent.com/15436444/37280318-709c891e-2613-11e8-8e76-9f81e0cfd214.png)

  ### 3. Next navigate as follows and create the reposiotory.
  
  Sign In -> Username & Password (Default username & password : admin / admin123 )
  
  Then click on Settings as shown in the below image.
  ![image](https://user-images.githubusercontent.com/15436444/37280512-f4b00c6c-2613-11e8-8898-ac33f59cb206.png)

  Then click on `Repositories` on the left pane and the click on `create repository` and then select `docker (hosted)`.
  
  And fill in the details as follows.
  
  ![image](https://user-images.githubusercontent.com/15436444/37280721-9ebdcd70-2614-11e8-8a29-8b87298c2da7.png)

  Finally Click on `Create repository`.
  
  Then the created repository will be shown as below.
  
  ![image](https://user-images.githubusercontent.com/15436444/37280774-d1e362c8-2614-11e8-9fe7-b0bb78a358ef.png)
  
  ### 4. Lets try to login to nexus reposiotory from docker node.
  
  Add the following condfiguration to docker.
  
  ```
  # cat /etc/docker/daemon.json
  {
      "insecure-registries" : ["nexus:9001"]
  }
  # systemctl restart docker
  #
  ```
  
  You might be execpected the following output.
  
  ![image](https://user-images.githubusercontent.com/15436444/37281545-6a2043a6-2617-11e8-940c-bb541599ad51.png)
  
  ### 5. Finally create an image and push to nexus repo and verify the repository.
  
  ```
  # docker tag centos nexus:9001/centos
  # docker push nexus:9001/centos
  The push refers to a repository [nexus:9001/centos]
  e15afa4858b6: Pushed
  latest: digest: sha256:7e94d6055269edb455bcfb637292573117e4a8341e9b9abbc09b17d8aafe8fbe size: 529
  ```
  ![image](https://user-images.githubusercontent.com/15436444/37281652-ce865132-2617-11e8-946c-a705229653c4.png)

  ## Hurray. Enjoy :)   
  
  
  
  
  
 
