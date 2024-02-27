# team-citydocker-docker-compose




# Fazendo a instalação do jetbrains-teamcity-server

# Criando um arquivo docker-compose.yml no instacia da AWS

version: "3"
services:
  teamcity-server:
    image: jetbrains/teamcity-server
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
      device: /home/ec2-user/teamcity/datadir
      o: bind
logs:
  driver: local
    driver_opts:
      type: none
      device: /home/ec2-user/teamcity/logs
      o: bind      
