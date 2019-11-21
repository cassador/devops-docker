Required steps:
  1. go to the build-server folder and run docker-compose up -d
  2. Jenkins and Nexus start might fail because of the permissions on volume mount path.
      a) to fix this issue go to the path as it is stated in docker-compose and run: chmod -R 777 <path> or change the ownership to jenkins
  3. To get jenkins admin password use docker logs jenkins
  4. To get nexus admin password go to the nexus docker container docker container:
      a) docker exec -it nexus /bin/bash
      b) cd /nexus-data
      c) cat admin.password
  5. Log into jenkins and install default plugins and change the admin password once that is done proceed with steps inside point 6.
  6. Go into jenkins container as root with command:
      a) docker exec -u 000 -it jenkins /bin/bash
      b) apt-get update
      c) apt-get install -qqy apt-transport-https ca-certificates curl gnupg2 software-properties-common
      d)  curl -fsSL https://download.docker.com/linux/debian/gpg | apt-key add -
      e)  apt-key fingerprint 0EBFCD88
      f)  add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/debian $(lsb_release -cs) stable"
      g)  apt-get update
      h)  apt-get install -qqy docker-ce
      i)  usermod -aG docker jenkins
      j)  curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | apt-key add -
      k)  cat <<EOF | tee /etc/apt/sources.list.d/kubernetes.list
      deb https://apt.kubernetes.io/ kubernetes-xenial main
      EOF
      l) apt-get install kubectl
      m) Verification steps:
        1) docker version
        2) kubectl version
  7. Inside jenkins in credentials section select Secret file and there upload the admin.conf from your kubernetes cluster ( to give access of Jenkins to multiple clusters with this type of credentials )
  8. Open nexus ui log with admin and create the docker repository as hosted and set the HTTP access on port 8082
  9. Create kubernetes secret using following command in your cluster:
     a)  kubectl create secret docker-registry regcred --docker-server=http://localhost:8082 --docker-username=<nexusUsername> --docker-password=<nexusPassword> --docker-email=<YourEmail>
  10. With step 9 when you will deploy application using jenkins based on previous steps it will allow to download the image.

If you would face any issue just open an issue part and i will check it as soon as i will have time, it is possible that i may have skipped some step during the process as i was not writing this readme after each step.
