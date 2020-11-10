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


![alt text](https://github.com/jardelkuhnen/MongoDB-ReplicaSet/blob/main/images/hostsMapeamento.png?raw=true)

3 - Após configurado os hosts, será necessário adicionar a keyserver para então realizarmos download do mongoDB.
  sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 68818C72E52529D4
  
4 - Então se faz necessário criar o arquivo de download no diretorio /etc/apt/sources.list.d/
  sudo echo "deb http://repo.mongodb.org/apt/ubuntu bionic/mongodb-org/4.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-4.0.list
  
5 - Atualize seu repositório:
  sudo apt-get update

6 - Agora iremos realizar a instação de fato do MongoDB 4.0
  sudo apt-get install -y mongodb-org
  
7 - Habilitando o servico de MongoDB para iniciar com linux e iniciando o servico de mongoDB:
  sudo systemctl enable mongod
  sudo systemctl start mongod
 
8 - Verificando se o servico iniciou normalmente: 
  sudo netstat -plntu

Verifique se irá aparecer o servico rodando na porta padrão 27017

Também é possível verificar via htop: 
  htop
	F4
	mongo

9 - Configurando MongoDB para acesso externo: 
  Abra o arquivo /etc/mongo.conf
  vim /etc/mongo.conf
  
  Acesse a tag net, e adicione o ip externo de sua máquina. Aqui também é possível realizar a troca de porta para acesso ao mongo.
  Após configurado, seu arquivo estará semelhante a imagem a seguir: 
  
![alt text](https://github.com/jardelkuhnen/MongoDB-ReplicaSet/blob/main/images/mongoConf.png?raw=true)


  
