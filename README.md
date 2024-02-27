# Team-citydocker-docker-compose

# 1 Criando um Security Group 
- Liberando as portas SSH e HTTP 
    - SSH para meu IP
    - HTTP para o mundo

# 2 Criando uma chave .PEM
- Salvar as credenciais 

# 3 Criando instancia 

- Usar a chave .PEM
- Security group 
- E colocar o script para rodar na instancia
  
```
#!/bin/bash

#Instalar Docker e Git
sudo yum update -y
sudo yum install git -y
sudo yum install docker -y
sudo usermod -a -G docker ec2-user
sudo usermod -a -G docker ssm-user
id ec2-user ssm-user
sudo newgrp docker

#Ativar docker
sudo systemctl enable docker.service
sudo systemctl start docker.service

#Instalar docker compose 2
sudo mkdir -p /usr/local/lib/docker/cli-plugins
sudo curl -SL https://github.com/docker/compose/releases/download/v2.23.3/docker-compose-linux-x86_64 -o /usr/local/lib/docker/cli-plugins/docker-compose
sudo chmod +x /usr/local/lib/docker/cli-plugins/docker-compose


#Adicionar swap
sudo dd if=/dev/zero of=/swapfile bs=128M count=32
sudo chmod 600 /swapfile
sudo mkswap /swapfile
sudo swapon /swapfile
sudo echo "/swapfile swap swap defaults 0 0" >> /etc/fstab


#Instalar node e npm
curl -fsSL https://rpm.nodesource.com/setup_21.x | sudo bash -
sudo yum install -y nodejs
```

# 4 Instalar a extensão RemoteSSH no visual code

- Conectar 
- Connect to host
- Configure SSH Hosts
- Caminho do seu arquivo
- Dar permissão para a chave .PEM Windows (cacls "nome do arquivo" /E /P Todos:F) ou Linux (chmod 400 "nome do arquivo")

- Host "nome para descrição" 
    - Hostname "hostname da instancia para acesso ssh" 
    - User "usuário da instancia" ec2-user
    - Port "porta solicitada" 22
    - IdentityFile "caminho onde está o seu arquivo .PEM" C:\Users\Vinicius\Desktop\"nome do arquivo"


# 5 Fazendo a instalação do jetbrains-teamcity-server

# 6 Criando um arquivo docker-compose.yml na instacia da AWS

- Criando a pasta teamcity no servidor
- mkdir teamcity
- cd teamcity
- mkdir datadir
- mkdir logs
- docker-compose up -d 


```
version: "3"
services:
  teamcity-server:
    image: jetbrains/teamcity-server
    restart: always (comando para caso desligar o servidor, quando ele ligar novamente iniciar a lista de comandos)
    container_name: teamcity-server-instance
    port: 
      - 80:8111
    volumes:
      - data_dir: /data/teamcity_server/datadir
      - logs: /opt/teamcity/logs
volumes:
  data_dir:
    driver: local
    driver_opts:
      type: none
      device: /home/ec2-user/teamcity/datadir (onde ira ficar na sua maquina)
      o: bind
logs:
  driver: local
    driver_opts:
      type: none
      device: /home/ec2-user/teamcity/logs
      o: bind  
```

