Pour éditer la configuration réseau et mettre à jour l'adresse IP  pour éviter les conflits, voici les étapes détaillées :

tout d'abbord extraire les VMs dans un fichier et les renommer en enlevant les caractères spéciaux parceque VirtualBox à un problème à les trouver avec les caractères spéciaux




Étape 1 : Installer et lancer les VMs

    Ouvrir VirtualBox :
        Lancez l'application VirtualBox sur votre ordinateur.

    Sélectionner 01_connect_box :
        Dans la liste des machines virtuelles, cliquez sur 01_connect_box pour la sélectionner.
    Sélectionner 01_connect_box_machine1 :
        Dans la liste des machines virtuelles, cliquez sur 01_connect_box_machine1 pour la sélectionner.
    Sélectionner 01_connect_box_machine2 :
        Dans la liste des machines virtuelles, cliquez sur 01_connect_box_machine2 pour la sélectionner.
 LANCER LES 3 VMS

Étape 2 : Configurer les Adresses IP de machine1 et machine2
Résoudre le Conflit d'Adresse IP

Le conflit d'adresse IP se produit car machine1 et machine2 ont la même adresse IP statique (192.168.0.2). Vous allez résoudre ce conflit en modifiant l'adresse IP de machine2.

    Démarrer machine2 :
        Retournez à la liste des machines virtuelles dans VirtualBox et démarrez machine2.

    Se Connecter à machine2 :
        Une fois le système démarré, connectez-vous avec les identifiants fournis :
            Nom d'utilisateur : root
            Mot de passe : un espace ( )



Étape 2 : Activer l’Attribution Dynamique d’IP sur machine2

Pour permettre à machine2 de recevoir une adresse IP dynamique via DHCP :

    Modifier le Fichier de Configuration Réseau à Nouveau :
        Répétez le processus pour accéder au fichier de configuration réseau.

    Avec /etc/network/interfaces :

    bash

nano /etc/network/interfaces

Configurer pour DHCP :

    Modifiez la configuration de INT_1 pour utiliser DHCP. Changez :

bash

iface INT_1 inet static
    address 192.168.0.2
    netmask 255.255.255.0
    gateway 192.168.0.1

à :

bash

iface INT_1 inet dhcp

Redémarrer l'Interface Réseau :

    Appliquez les changements en redémarrant le service réseau de la même manière que précédemment :

bash

    systemctl restart networking

redémarrer le système pour bien enregistrer la configuration


Vérification de la Connectivité

    Vérifier la Connexion :
        Vous pouvez maintenant vérifier la connectivité en pingant un site Web, par exemple Google :

    bash

timeout --signal SIGINT 1m ping google.com
