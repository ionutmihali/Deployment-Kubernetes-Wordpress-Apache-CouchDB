Am urmat pasii 1-7 din laboratorul 9, pentru crearea unui mini-cluster Kubernetes și rularea unui site web pe mai multe mașini cu suport load balance și autoscale.

Am creat un deployment de Wordpress: https://kubernetes.io/docs/tutorials/stateful-application/mysql-wordpress-persistent-volume/

Am creat o imagine docker pentru server apache, care sa includa librariile de lucru cu CouchDB, folosind Dockerfile-ul prezent in arhiva si fisierul index.php, ruland comenzile:
docker build -t TAG .
docker tag TAG localhost:32000/TAG
docker push localhost:32000/TAG

Am recreat alias-ul: alias kubectl='microk8s kubectl' si am mai rulat o data comanda pentru LoadBalancer: microk8s enable metallb:IP_PRIVAT_KUBE1-IP_PRIVAT_KUBE2

Am creat un deploymnet pentru Apache cu PHP: https://medium.com/akeo-tech/deploy-php-applications-using-kubernetes-870c87c0acf0

Am creat un deployment pentru CouchDB: https://faun.pub/deploying-a-couchdb-cluster-on-kubernetes-d4eb50a08b34

In Azure, sectiunea Networking a VM, am adaugat la Inbound port rule, porturile pe care ruleaza serviciile: wordpress(80), mysql(3306), apache(88), couchdb(30984).

In CouchDB, din interfata, am creat baza de date: chat
In Wordpress, din interfata, am creat website-ul, am stilizat si apoi am introdus un iframe catre chat-ul de pe serverul Apache: <iframe src="http://localhost:88" style="width: 100%; height: 500px;"></iframe>
In index.php, se regasesc conexiunea la baza de date, interogarea acesteia, cat si chat-ul propriu-zis, alaturi de un istoric al mesajelor.
