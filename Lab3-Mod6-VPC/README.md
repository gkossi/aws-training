# AWS-TRAINING

-----------------------------------------------------------------------------------------
# TP N°3/Lab-3 : VPC
-----------------------------------------------------------------------------------------
Un peu de contexte :
ici, il est question de réaliser une insfrastructure réseau résiliante c'est à dire une insfrastructure hautement disponible.
On a les zones de disponibilité et également les régions qui sont en quelques sorte la limite de notre insfrastructure sur une région donnée dans un pays donné.
Alors, pour mettre en place une infrastructure hautement disponible, généralement, on va avoir 2 availability zones qui vont contenir nos applications.

TAF : 
--- 
Dans notre contexte, nous souhaitons mettre en place un réseau publique(accessible depuis l'extérieur)/privé(non accessible depuis l'extérieur) sur une zone de disponibilité A et également reproduire la meme chose dans une autre zone de disponibilité B afin qu'en cas de problème sur une zone de diponibilité, l'on puisse continuer à exécuter notre application sur l'autre zone de diponibilité.

Pour la 1ère zone, on aura un composant NAT (NAT gateway) pour permettre à ceux qui sont dans le réseau privé de pouvoir accéder à internet mais que le sens inverse soit impossible.

-----------------------------------------------------------------------------------------
# A retenir:
-----------------------------------------------------------------------------------------

*Etape1 : Créer la 1ère partie de l'infrastructure dans une 1ère zone de disponibilité
------------------------------------------------------
- Sur la console AWS, choisir le service VPC pour un VPC avec la plage d'adresse 10.0.0.0/16
- Ensuite, créer un réseau publique1 (10.0.0.0/24) et un réseau privé1 (10.0.1.0/24) dans la zone de disponibilité us-east-1a
- Créer un NAT gateway à partir d'une instance ec2 de type t2.nano

*Etape2 : Créer la 2è partie de l'infrastructure - les sous-réseau publique et privé dans une seconde zone de disponibilité
------------------------------------------------------
- Créer un réseau publique2 (10.0.2.0/24) et un réseau privé2 (10.0.3.0/24) dans la zone de disponibilité us-east-1b

*Etape3 : Configurer la table de routage pour permettre aux réseaux publiques 1&2 de passer par l'internet gateway pour accéder à internet et les réseaux privés 1&2 de passer par la NAT gateway pour accéder à internet
------------------------------------------------------

*Etape4 : Créer un security group à assigner au VPC
------------------------------------------------------
- autoriser le trafique entrant en HTTP

*Etape5 : Créer une instance EC2
------------------------------------------------------
- Créer une instance EC2 de type t2.micro
- Assigner le VPC créé
- Assigner le 1er sous-réseau publique dans la 1ère zone de disponibilité
- Assigner une adresse IP publique automatiquement
- Mettre le code suivant dans user data pour installer automatiquement le serveur web après déploiement de l'instance :
*#!/bin/bash
*# Install Apache Web Server and PHP
*yum install -y httpd mysql php
*# Download Lab files
*wget https://aws-tc-largeobjects.s3.amazonaws.com/AWS-TC-AcademyACF/acf-lab3-vpc/lab-app.zip
*unzip lab-app.zip -d /var/www/html/
*# Turn on web server
*chkconfig httpd on
*service httpd start

- Attribuer le security group créé à notre instance


