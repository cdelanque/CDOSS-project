Sujet : installation de MySQL sur OpenStack

__Partie 1__
**Question 1 : Lors du provisionnement d’une instance OpenStack destinée à héberger MySQL, quels éléments sont techniquement nécessaires ou recommandés pour automatiser une installation propre via OpenStack CLI et cloud-init ?**
Lien d’aide : https://docs.openstack.org/nova/latest/user/launch-instances.html
*A. Définir un flavor, une image, un réseau, une clé SSH et un security group lors de la création de l’instance.*
*B. Utiliser l’option `--user-data` pour transmettre un script cloud-init capable d’installer et de configurer MySQL au premier démarrage.*
*C. Ouvrir obligatoirement le port TCP 3306 à `0.0.0.0/0` pour permettre l’installation des paquets MySQL.*
*D. Prévoir une image compatible cloud-init si l’on veut injecter une clé SSH ou un script de personnalisation au démarrage.*
*E. Utiliser uniquement le disque éphémère du flavor pour les données MySQL de production, car il est automatiquement indépendant du cycle de vie de l’instance.*
**Question 2 : Pour installer MySQL dans une VM OpenStack avec les données stockées sur un volume Cinder dédié, quelles affirmations sont correctes ?**
Lien d’aide : https://docs.openstack.org/cinder/latest/admin/manage-volumes.html
*A. Un volume Cinder peut être créé puis attaché à une instance avec une commande de type `openstack server add volume`.*
*B. Après attachement, le volume apparaît généralement dans le système invité comme un périphérique bloc, par exemple `/dev/sdX`, qu’il faut partitionner, formater et monter.*
*C. Pour placer le répertoire de données MySQL sur ce volume, il faut arrêter MySQL, déplacer ou initialiser le `datadir`, adapter la configuration MySQL et vérifier les droits du compte système `mysql`.*
*D. Une entrée `/etc/fstab` fiable, idéalement basée sur UUID, est utile pour remonter le volume au redémarrage avant le démarrage effectif de MySQL.*
*E. Un snapshot Cinder pris pendant une forte activité d’écriture garantit toujours une sauvegarde logique cohérente de MySQL, sans aucune précaution côté base.*
**Question 3 : Pour exposer MySQL installé sur une VM OpenStack de manière sécurisée, quelles affirmations sont correctes concernant le réseau et les security groups ?**
Lien d’aide : https://docs.openstack.org/nova/latest/user/security-groups.html
*A. Un security group fonctionne comme une liste de règles d’autorisation : le trafic entrant qui ne correspond à aucune règle autorisée est refusé par défaut.*
*B. Le port TCP 3306 doit généralement être limité aux serveurs applicatifs, aux bastions ou aux sous-réseaux d’administration autorisés, et non exposé publiquement sans filtrage.*
*C. Pour une réplication MySQL asynchrone classique, les flux entre nœuds doivent être autorisés entre les instances concernées, généralement sur le port MySQL configuré.*
*D. L’utilisation d’une floating IP rend automatiquement l’instance hautement disponible même en cas de perte du compute node hébergeant la VM.*
*E. Pour réduire les risques d’indisponibilité, des instances MySQL répliquées devraient être placées sur des hôtes ou zones différents lorsque les mécanismes OpenStack le permettent.*

__Partie 2__
Question 1 : Réponse : A, B, D
*Explication : Pour créer une instance exploitable, il faut choisir les ressources et paramètres OpenStack essentiels, notamment le flavor, l’image, le réseau, la clé SSH et le security group. L’option `--user-data` permet de fournir un script de personnalisation, souvent interprété par cloud-init, pour automatiser l’installation de MySQL. En revanche, ouvrir le port 3306 à tout Internet n’est pas nécessaire pour installer les paquets et représente un risque. Le disque éphémère du flavor n’est pas le meilleur choix pour les données MySQL de production, car il est fortement lié au cycle de vie et au placement de l’instance.*
Question 2 : Réponse : A, B, C, D
*Explication : Cinder fournit du stockage bloc persistant qui peut être attaché à une instance. Dans la VM, ce volume doit être préparé comme un disque classique : partitionnement éventuel, système de fichiers, montage, droits et configuration MySQL. Pour utiliser ce volume comme `datadir`, il faut contrôler l’arrêt du service, la cohérence des fichiers, le chemin configuré et les permissions. Une entrée `fstab` robuste évite que MySQL démarre avec un point de montage absent. Un snapshot Cinder seul n’est pas forcément une sauvegarde logique cohérente si MySQL écrit activement au moment de la capture.*
Question 3 : Réponse : A, B, C, E
*Explication : Les security groups OpenStack autorisent explicitement certains flux et bloquent le reste du trafic entrant par défaut. Pour MySQL, il est recommandé de limiter le port 3306 aux consommateurs légitimes : application, administration ou réplication. En réplication asynchrone classique, les nœuds doivent pouvoir communiquer sur le port MySQL configuré. Une floating IP facilite l’accès externe mais ne transforme pas une VM seule en service hautement disponible. La haute disponibilité exige plutôt une architecture multi-instances, idéalement répartie sur plusieurs hôtes ou zones.*

__*Sous licence CC BY - Mise à jour le 16/06/2026*__
