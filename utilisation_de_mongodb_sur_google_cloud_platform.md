**Partie 1**  
  **Question 1 : Pour un déploiement MongoDB auto-géré sur Google Compute Engine, avec WiredTiger et une charge OLTP générant beaucoup d’E/S aléatoires, quels choix de stockage sont techniquement cohérents ?**  
Lien d'aide : https://cloud.google.com/compute/docs/disks/performance  
_A. Utiliser prioritairement un Standard Persistent Disk, car il est optimisé pour les forts volumes d’IOPS aléatoires._  
_B. Privilégier un SSD Persistent Disk, un Extreme Persistent Disk ou une option Hyperdisk adaptée lorsque la charge exige des IOPS aléatoires élevées._  
_C. Dimensionner conjointement la taille du disque et le nombre de vCPU, car les limites d’IOPS et de débit dépendent à la fois du stockage provisionné et de la VM._  
_D. Éviter de considérer le striping manuel comme obligatoire, car Compute Engine optimise déjà les performances des Persistent Disks et recommande plutôt d’augmenter la taille du disque ou les ressources VM si nécessaire._  
_E. Utiliser uniquement le disque de démarrage standard de petite taille pour héberger les données, les journaux et l’oplog d’une base MongoDB de production._  
  **Question 2 : Dans MongoDB Atlas sur Google Cloud, quelles affirmations sont correctes concernant l’accès privé via Private Service Connect ?**  
Lien d'aide : https://www.mongodb.com/docs/atlas/security-private-endpoint/?cloud-provider=gcp  
_A. Les clusters Free et Flex ne prennent pas en charge les connexions via private endpoint._  
_B. Le private endpoint doit être configuré dans la même région que le cluster Atlas cible._  
_C. Pour un cluster multi-région, il faut prévoir un private endpoint pour chaque région contenant un nœud._  
_D. Les chaînes de connexion optimisées pour sharded clusters derrière private endpoint sont prises en charge sur Google Cloud exactement comme sur AWS._  
_E. Après configuration d’un private endpoint, les rôles Atlas, la sécurité applicative et la gouvernance des accès deviennent inutiles._  
  **Question 3 : Pour sécuriser un replica set MongoDB auto-géré sur des VM Google Compute Engine, quelles mesures sont techniquement pertinentes ?**  
Lien d'aide : https://www.mongodb.com/docs/manual/administration/security-checklist/  
_A. Ouvrir le port 27017 à 0.0.0.0/0 pour simplifier l’administration, puis compter uniquement sur le mot de passe MongoDB._  
_B. Activer le contrôle d’accès, l’authentification et le RBAC afin d’éviter les connexions anonymes ou les comptes applicatifs trop privilégiés._  
_C. Configurer une authentification interne entre membres du replica set, par exemple avec keyfile ou certificats X.509 selon le niveau d’exigence._  
_D. Restreindre les flux réseau vers MongoDB aux serveurs applicatifs, aux bastions d’administration et aux membres du replica set nécessaires._  
_E. Utiliser un compte applicatif unique avec le rôle root pour éviter de gérer plusieurs rôles MongoDB._  
**Partie 2**  

Question 1  
Réponse : B, C, D  
_Explication : Pour une charge MongoDB transactionnelle avec de nombreuses E/S aléatoires, un disque standard n’est généralement pas le meilleur choix. Les options SSD, Extreme Persistent Disk ou Hyperdisk selon le besoin permettent de viser de meilleures performances. Le dimensionnement doit aussi prendre en compte la taille du disque, le type de disque et les limites liées à la VM, notamment les vCPU et le débit maximal._
Question 2  
Réponse : A, B, C  
_Explication : Sur Google Cloud, MongoDB Atlas utilise Private Service Connect pour les connexions privées. Les clusters Free et Flex ne sont pas éligibles. Le private endpoint doit être aligné avec la région du cluster, et un cluster multi-région nécessite une conception région par région. Les chaînes de connexion optimisées pour sharded clusters derrière private endpoint ne sont pas disponibles sur Google Cloud comme sur AWS._
Question 3  
Réponse : B, C, D  
_Explication : Un replica set MongoDB auto-géré sur Google Cloud doit être protégé à plusieurs niveaux : authentification et RBAC côté MongoDB, authentification interne entre membres, et filtrage réseau côté VPC/firewall. Exposer directement le port MongoDB sur Internet ou utiliser un compte applicatif root augmente fortement le risque d’accès non autorisé et de compromission._

*Sous [licence CC BY](https://creativecommons.org/licenses/by/4.0/) - Mise à jour le 16/06/2026*
