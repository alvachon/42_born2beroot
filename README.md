# BORN2BEROOT  ![alvachon's 42 Born2beroot Score](https://badge42.vercel.app/api/v2/clb9zrpvt00250fl97rqy9hie/project/2676536) 
![VM](https://img.shields.io/badge/VirtualBox-21416b?style=for-the-badge&logo=VirtualBox&logoColor=white) ![Debian](https://img.shields.io/badge/Debian-A81D33?style=for-the-badge&logo=debian&logoColor=white) ![GNU](https://img.shields.io/badge/GNU%20Bash-4EAA25?style=for-the-badge&logo=GNU%20Bash&logoColor=white) ![PHP](https://img.shields.io/badge/PHP-777BB4?style=for-the-badge&logo=php&logoColor=white) ![MARIADB](https://img.shields.io/badge/MariaDB-003545?style=for-the-badge&logo=mariadb&logoColor=white) ![WP](https://img.shields.io/badge/Wordpress-21759B?style=for-the-badge&logo=wordpress&logoColor=white)

## Guide to create your own virtual machine with debian operating system. 

# **General Instruction**

## How to keep the same signature
Before sending de project:
- Restore snapshot, do not open it
- Take the .vdi file of borntoberoot
- wait (6 min)
- Send this signature
```
 born2beroot.vdi
 ```

**Before evaluating**

- start
- Take the .vdi file
- check the signature
- at the end, close everything, close + restore snapshot option

# **Mandatory part**

## Qu’est-ce qu’une machine virtuelle, comment cela fonctionne ?
**Une machine virtuelle est un fichier qui se comporte comme un ordinateur.**
    
Pour que cela fonctionne, il faut utiliser un programme qui va procéder à la virtualisation du fichier en empruntant les ressources de la machine hôte (CPU, espace de stokage, mémoire . . . ). En utilisant de nouvelles partitions, on rend possible l’isolement des différents systèmes et de créer des environnements controlé. 

Il devient donc possible d’installer un différent OS de l’ordinateur, de faire fonctionner des programmes qui ne fonctionneraient pas normalement sur notre machine-hôte, de tester des applications sans changer notre environnement de travail ou de voir le comportement d’un virus informatique de façon sécuritaire.
    
Le programme contient généralement une fonctionnalité appelé hyperviseur qui agit comme un manager de ressources et rend possible d’avoir plusieurs machines virtuelles avec différents OS. Il existe 2 types d’hyperviseurs. Le type 1 permet d’opérer le système sur l’espace physique de la machine hôte alors que le type 2 agit plutôt comme un programme informatique.
    
Le programme peut être installé en local sur un ordinateur personnel, mais il peut également être hébergé sur un cloud (serveur en remote).
    
Dans le cadre du projet, nous utilisons Virtual Box, qui est accessible à tous gratuitement car il est open source et qui utilise un hyperviseur de type 2.
    
## Qu’elle est l’utilité d’une machine virtuelle ?
    
- Dans le cadre du travail d’un.e developpeur.e, une partie du déploiement d’un projet est de réaliser des tests dans un environnement contrôlé. Travailler avec les VMs permet cela rapidement, sans devoir investir dans l’infrastructure informatique.

- La possibilité de faire un backup de notre installation actuelle sur une VM permet d’éviter les arrêts de travail aléatoire et d’avoir une sécurité supplémentaire pour conserver le matériel.

- Augmenter la sécurité contre les attaques informatiques.
    

## **Apt  (Advanced Packaging Tool)**

Est un installateur de paquet. Permet d’installer ou de supprimer des programmes. Il est appelé à partir de la ligne de commande

## **Aptitude**

Est aussi un installateur de paquets, mais provient avec une interface menu. Plus riche, plus d’options, plus intuitif. Par contre, call syntaxique différentes de apt.

## **APPARMOR**

AppArmor permet à l'[administrateur système](https://fr.wikipedia.org/wiki/Administrateur_syst%C3%A8me) d'associer à chaque programme un profil de sécurité qui restreint ses accès au [système d'exploitation](https://fr.wikipedia.org/wiki/Syst%C3%A8me_d%27exploitation).

## **UFW**

Firewall pour les tables de IPs. (Iptables) Permet de configurer des règles et des chaînes en Kernel (core du OS). C’est le système le moins compliqué et le plus user-friendly pour les utilisateura hosts. On peut faire des actions sur la ligne de commande.

## **SSH - openssh server**

Permet des connextions sécuriséses sur un réseau informatique grace au protocole ssh (facilitateur de connextions sécurisées entre 2 systèmes (client/serveur) pour se connecter à distance)

**PHP  :** Language de programmation pour le développement web

**Lighttpd :** Serveur web http pour travailler en localhost

**Maria db :** Database sql (Gestionnaire de données utilisé dans ce cadre-ci pour loger les informations générées par le wordpress)

**Wordpress :** Systeme de gestion de contenu, utilisé pour constuire des sites, blogues, apps . . . Fonctionne avec PHO et SQL

**Fail2ban :** Framework de prévention contre les intrusions (bloque les adresses ips après plusieurs attentes en ajoutant une regle iptable) Cherche les erreurs d’authentifications. Ralenti les attaques de forces brutes ou de déni de service
