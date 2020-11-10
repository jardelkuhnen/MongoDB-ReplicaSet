# MongoDB-ReplicaSet
Criando replicaset com mongoDB

A seguir será configurado dois replicaSet e um árbitro.

#### 1 - Realizar update e upgrade das maquinas antes de iniciar:
  > sudo apt-get update
  > sudo apt-get upgrade
  
#### 2 - Será necessário editar o arquivo /etc/hosts para que as maquinas tenham acesso na rede via hostName:
  > vim /etc/hosts
  
  > Insira ip e hostName. 

* Após configurado seu arquivo ficará semelhante a imagem a seguir: 

![alt text](https://github.com/jardelkuhnen/MongoDB-ReplicaSet/blob/main/images/hostsMapeamento.png?raw=true)

#### 3 - Após configurado os hosts, será necessário adicionar a keyserver para então realizarmos download do mongoDB.
  > sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 68818C72E52529D4
  
#### 4 - Então se faz necessário criar o arquivo de download no diretorio /etc/apt/sources.list.d/
  > sudo echo "deb http://repo.mongodb.org/apt/ubuntu bionic/mongodb-org/4.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-4.0.list
  
#### 5 - Atualize seu repositório:
  > sudo apt-get update

#### 6 - Agora iremos realizar a instação de fato do MongoDB 4.0
  > sudo apt-get install -y mongodb-org
  
#### 7 - Habilitando o servico de MongoDB para iniciar com linux e iniciando o servico de mongoDB:
  > sudo systemctl enable mongod
  > sudo systemctl start mongod
 
#### 8 - Verificando se o servico iniciou normalmente: 
  > sudo netstat -plntu

* Verifique se irá aparecer o servico rodando na porta padrão 27017

 Também é possível verificar via htop: 
  > htop
  > F4
  > mongo

#### 9 - Configurando MongoDB para acesso externo: 
  > Abra o arquivo /etc/mongo.conf
  > vim /etc/mongo.conf
  
  Acesse a tag net, e adicione o ip externo de sua máquina. Aqui também é possível realizar a troca de porta para acesso ao mongo.
  Após configurado, seu arquivo estará semelhante a imagem a seguir: 
  
![alt text](https://github.com/jardelkuhnen/MongoDB-ReplicaSet/blob/main/images/mongoConf.png?raw=true)


#### 10 - Após realizado essa configuração em todas as maquinas do replicaSet, incluindo o arbitro, será necessário reiniciar os servico do mongo: 
   > sudo service mongod restart
	
# CONFIGURANDO REPLICA SET E ÁRBITRO

#### 1 - Acesse o mongo, via linha de comando na máquina que será o primário: 
   > mongo –-port 38128

#### 2 - Inicialize o replicaSet
   > rs.initiate()

#### 3 - Valide as configuracoes atuais de seu replicaSet:
   > rs.config()
   
#### 4 - Será exibido algo semelhante a imagem a seguir: 

![alt text](https://github.com/jardelkuhnen/MongoDB-ReplicaSet/blob/main/images/replicaSetConfigurationInitial.png?raw=true)

#### 5 - Agora iremos adicionar cada maquina ao replicaSet:
   > rs.add(ipMongoReplica02:portaMongo)

#### 6 - Após adicionado verifique novamente a configuração: 
   > rs.config()
   
Será exibido algo semelhante a imagem a seguir: 
![alt text](https://github.com/jardelkuhnen/MongoDB-ReplicaSet/blob/main/images/replicaSetConfiguration.png?raw=true)

#### 7 - Agora será adicionado o árbitro: 
   > rs.addArb(“ipMongoArbitro:portaMongo”)

#### 8 - Verifique novamente a configuração do seu replicaSet e verifique se o arbitro está lá: 
   > rs.config()
   
#### 9 - Enfim tudo configurado. Agora para um teste final, acesse por algum cliient de mongo, como [NoSqlBooster](https://nosqlbooster.com/)
  
  Exemplo de url utilizada para acessar seu replicaSet: mongodb://ip:port,ip:port,ip:port/?retryWrites=true&replicaSet=replicaSet

Tudo certo e funcionando, bora tomar uma cerveja.

![alt text](https://github.com/jardelkuhnen/MongoDB-ReplicaSet/blob/main/images/beer.jpg?raw=true)

   

