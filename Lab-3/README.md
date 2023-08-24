# AWS-TRAINING

-----------------------------------------------------------------------------------------
# TP N°3/Lab-3 : Création d'une VM
-----------------------------------------------------------------------------------------
TAF : Création d'une VM
*Création d'une VM et ensemble des étapes détailées pour savoir comment déployer une VM à l'aide de bonnes pratiques*
- Comment resizer une VM ?
- Comment déployer une VM ?
- Comment configurer les security groups ?
- Comment installer directement des applications après le déploiement de la VM ?

-----------------------------------------------------------------------------------------
# A retenir:
-----------------------------------------------------------------------------------------
- Sur la console AWS, Aller dans services et rechercher ec2
- Aller ensuite sur l'onglet instances pour créer une nouvelle instance
- Choisir une image linux par défaut
- Choisir le gabarit par défaut

- Choisir les caractéristiques de la VM
  .Activer l'assignation d'une IP publique
  .Activer la protection contre la suppression accidentelle
  
- Insérer le script suivant dans le champ "User date" pour installer directement le serveur web :

#!/bin/bash
On va tester voir si le script marche en essayant de créer un répertoire dans /home/ec2-user/
mkdir /home/ec2-user/weberserver
yum -y install httpd
systemctl enable httpd
systemctl start httpd
echo '<html><h1>Hello From Your Web Server!</h1></html>' > /var/www/html/index.html

NB : Ce script permet d'installer httpd et de créer une page test dans index.html

- Pour la partie disque dur, il faut laisser par défaut la capacité de 8Go
- Créer par exemple un tag "Name" pour donner un nom à la VM (exemple : WebServer)

- Aller ensuite sur security group  pour le configurer





