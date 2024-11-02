

1. Executez la commande **minikube start --nodes 3 --driver=docker** pour lancer 3 nodes : 1 controle plane et 2 worker *(si le cluster architecture existe deja alors executez minikube node add pour creer un nouveau noeud)*

2. Rendez vous dans le dossier **lab-kubernetes** une fois le projet cloné

Refactoring avec 1 seul noeud 

3. Executez les commandes suivantes : ( de preference avec une architecture a un seul noeud)
   - ***alias kbc="kubectl"*** 
   - ***kbc apply -f backend-secret.yaml***  
   - ***kbc apply -f database-secret.yaml***  
   - ***kbc apply -f database-deployment.yaml***
   - ***kbc apply -f database-service.yaml***
   - ***kbc apply -f network-policy.yaml***   
   - ***kbc apply -f backend-deployment.yaml***
   - ***kbc apply -f backend-service.yaml***

Une fois les commandes executez , verifiez bien que  3 pods sont crées : 2 backend et un database

Executez : ***kbc get pod -o wide"***
Pour voir sur quel noeud les pods sont execute
Executez : ***kbc get pod "***
Pour voir l'etat actuel : initialemnt les pods backend vont attendre que la base soit initialisée pour demarrer

Attendre quelques seconds les initContainer terminent leur process

 

Le service pour exposer l'application ecoute sur le port 30000

Executez la commande pour recuperer l'adresse IP des nodes

***kbc get node -o wide***

Recuperez l'adresse IP du noeud control plane . Exemple pour mon cas : 192.168.7.2

Ouvez votre navigateur et saisir : 192.168.7.2:30000

!! vous avez access à l'application

**Troubleshooting**
Dans mon cas l'architecture 1 a un seul noeud a pu marché \n
Mais lorsque je passe à une architecture de plusieurs noeuds, la base donnée ainsi que les pods backend ont des status crashLoopBackOff
J'ai beau essayé faire des modifications , mais tjrs rien !