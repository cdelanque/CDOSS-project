__Partie 1 : Questions__

**Question 1. Sur une VM Azure en mode IaaS, quelles affirmations décrivent correctement l’utilisation de MongoDB Community ou Enterprise ?**
*A. L’administrateur choisit l’image de VM, le système d’exploitation, les disques et installe lui-même MongoDB.*
*B. Azure installe automatiquement MongoDB Community ou Enterprise dès que la VM est créée.*
*C. L’administrateur doit gérer les mises à jour MongoDB, la configuration, la sécurité et les sauvegardes applicatives.*
*D. MongoDB Enterprise peut apporter des fonctionnalités supplémentaires par rapport à Community, notamment autour de la sécurité et de l’administration selon l’édition utilisée.*
*E. En IaaS, MongoDB est nécessairement un service SaaS entièrement opéré par MongoDB Atlas.*
Lien d’aide : <https://www.mongodb.com/docs/manual/installation/>

**Question 2. Pour stocker les données MongoDB sur une VM Azure, quelles pratiques sont généralement pertinentes ?**
*A. Utiliser des disques managés Azure adaptés aux besoins d’IOPS, de débit et de latence.*
*B. Séparer autant que possible le disque du système d’exploitation et les disques de données MongoDB.*
*C. Choisir le type de disque uniquement selon le prix, sans tenir compte de la charge d’écriture et de lecture.*
*D. Surveiller les métriques disque et VM, car les performances MongoDB dépendent aussi du stockage sous-jacent.*
*E. Placer toutes les données MongoDB uniquement sur un disque temporaire Azure pour bénéficier d’une persistance maximale.*
Lien d’aide : <https://learn.microsoft.com/fr-fr/azure/virtual-machines/managed-disks-overview>

**Question 3. Pour obtenir de la haute disponibilité avec MongoDB sur des VM Azure, quelles affirmations sont correctes ?**
*A. Un replica set MongoDB permet d’avoir plusieurs processus mongod maintenant le même jeu de données.*
*B. Un replica set peut améliorer la disponibilité en cas de perte d’un serveur de base de données.*
*C. Déployer tous les membres du replica set sur une seule VM suffit pour se protéger contre la panne de cette VM.*
*D. Répartir les membres sur plusieurs VM, idéalement sur des zones de disponibilité Azure lorsque c’est possible, renforce la résilience.*
*E. Un replica set supprime définitivement le besoin de sauvegardes.*
Lien d’aide : <https://www.mongodb.com/docs/current/replication/>

__Partie 2 : Réponses et explications__

Question 1 — Réponse : A, C, D
*Explication : En mode IaaS, Azure fournit principalement l’infrastructure de VM, mais l’installation et l’administration de MongoDB restent à la charge de l’équipe qui exploite la VM. MongoDB Enterprise peut offrir des fonctionnalités supplémentaires par rapport à Community selon les besoins de sécurité, d’administration et de support. MongoDB Atlas correspond plutôt à une offre managée, différente d’une installation auto-administrée sur VM IaaS.*
Question 2 — Réponse : A, B, D
*Explication : Les performances de MongoDB dépendent fortement du stockage. Sur Azure, il est pertinent d’utiliser des disques managés adaptés à la charge, de séparer le système et les données, puis de surveiller les métriques de disque et de VM. Un disque temporaire ne doit pas être utilisé comme stockage persistant principal pour les données MongoDB.*
Question 3 — Réponse : A, B, D
*Explication : Un replica set MongoDB fournit redondance et haute disponibilité grâce à plusieurs membres maintenant le même jeu de données. Pour résister à la panne d’une VM, les membres doivent être répartis sur plusieurs VM, et si possible sur plusieurs zones de disponibilité Azure. Un replica set ne remplace pas une stratégie de sauvegarde, car il réplique aussi les erreurs logiques ou suppressions accidentelles.*