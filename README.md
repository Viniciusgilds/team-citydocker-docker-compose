# team-citydocker-docker-compose




# Fazendo a instalação do jetbrains-teamcity-server

# Criando um arquivo docker-compose.yml no instacia da AWS

- Criando a pasta teamcity no servidor
- mkdir teamcity
- cd teamcity
- mkdir datadir
- mkdir logs
- docker-compose up -d 

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
