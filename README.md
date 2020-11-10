# MongoDB-ReplicaSet
Criando replicaset com mongoDB

A seguir será configurado dois replicaSet e um árbitro.

1 - Realizar update e upgrade das maquinas antes de iniciar:
  sudo apt-get update
  sudo apt-get upgrade
  
2 - Será necessário editar o arquivo /etc/hosts para que as maquinas tenham acesso na rede via hostName:
  vim /etc/hosts
  
  Insira ip e hostName. 

Após configurado seu arquivo ficará semelhante a imagem a seguir: 

