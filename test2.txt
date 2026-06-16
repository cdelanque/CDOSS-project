__Partie 1__
**Question 1. Dans MySQL Enterprise Audit, quelles actions permettent de mettre en place un audit trail serveur capable de journaliser les connexions et les requêtes tout en filtrant finement les événements ?**
Lien d’aide : https://dev.mysql.com/doc/refman/8.4/en/audit-log-filtering.html
*A. Installer le plugin ou composant d’audit Enterprise, puis installer les tables et fonctions d’audit nécessaires au filtrage.*
*B. Définir un filtre avec audit_log_filter_set_filter(), puis l’associer à un compte ou au compte générique % avec audit_log_filter_set_user().*
*C. Activer uniquement le general_log, car il fournit nativement des règles de filtrage JSON persistantes par utilisateur.*
*D. Stocker les filtres d’audit dans les tables système prévues, par défaut dans la base mysql, sauf configuration différente.*
*E. Créer seulement des triggers AFTER INSERT, AFTER UPDATE et AFTER DELETE sur chaque table métier pour capturer les connexions, les échecs d’authentification et les commandes DDL.*
**Question 2. Pour créer un audit trail applicatif par triggers sur une table InnoDB critique, quelles affirmations sont techniquement correctes ?**
Lien d’aide : https://dev.mysql.com/doc/refman/8.4/en/create-trigger.html
*A. Un trigger AFTER UPDATE peut lire les valeurs OLD et NEW pour écrire dans une table d’audit l’ancienne valeur, la nouvelle valeur, l’utilisateur logique et l’horodatage.*
*B. Un trigger BEFORE DELETE ne peut jamais lire OLD, car la ligne est déjà supprimée au moment de son exécution.*
*C. Un modèle robuste sépare la table métier et la table d’audit, et évite de modifier récursivement la même table métier depuis son propre trigger.*
*D. Les triggers suffisent à auditer toutes les commandes SELECT, GRANT, CREATE USER et les tentatives de connexion échouées.*
*E. Les triggers d’audit participent à la transaction : si la transaction métier est annulée, l’écriture d’audit réalisée dans la même transaction est généralement annulée aussi.*
**Question 3. Dans une stratégie d’audit trail basée sur le binary log MySQL et une exploitation de type CDC, quelles affirmations sont correctes pour conserver une trace exploitable des changements de données ?**
Lien d’aide : https://dev.mysql.com/doc/refman/8.4/en/replication-options-binary-log.html
*A. Le format ROW est le format adapté pour capturer les changements ligne à ligne, car les événements binaires décrivent les modifications de lignes plutôt que seulement le texte SQL.*
*B. La variable binlog_row_image=full permet de journaliser davantage d’informations de ligne que minimal, ce qui peut aider à reconstruire les états avant/après au prix d’un volume de logs plus important.*
*C. Le binary log remplace complètement un audit trail de sécurité, car il capture nativement les connexions échouées, les lectures SELECT et toutes les décisions d’autorisation.*
*D. La rétention des fichiers binaires doit être pilotée, par exemple avec binlog_expire_logs_seconds, sinon l’audit CDC peut perdre l’historique nécessaire ou saturer le stockage.*
*E. Désactiver log_bin est recommandé pour un audit trail CDC, car cela force MySQL à écrire les événements DML dans le general_log au format ligne.*
__Partie 2__
Question 1 — Réponse : A, B, D
*Explication : MySQL Enterprise Audit fournit un mécanisme serveur dédié à l’audit des événements, avec des fonctions de filtrage telles que audit_log_filter_set_filter() et audit_log_filter_set_user(). Les règles sont persistées dans des tables d’audit, par défaut dans la base mysql. Le general_log n’offre pas le même modèle de filtrage d’audit Enterprise, et les triggers ne permettent pas de capturer correctement les connexions, les échecs d’authentification ou toutes les commandes serveur.*
Question 2 — Réponse : A, C, E
*Explication : Les triggers permettent de capturer des modifications DML sur les tables métier et d’insérer des lignes dans une table d’audit avec OLD, NEW, un horodatage ou un utilisateur applicatif. OLD est disponible pour DELETE et UPDATE, NEW est disponible pour INSERT et UPDATE. En revanche, les triggers ne capturent pas les lectures SELECT, les connexions, les échecs d’authentification ou les commandes d’administration. Comme ils s’exécutent dans le contexte de la transaction, une annulation de transaction annule généralement aussi l’écriture d’audit réalisée par le trigger.*
Question 3 — Réponse : A, B, D
*Explication : Le binary log en format ROW est utile pour une approche CDC, car il encode les changements de lignes. Avec binlog_row_image=full, les images de lignes sont plus complètes, ce qui facilite certaines reconstructions mais augmente le volume de stockage. La rétention doit être dimensionnée et surveillée. En revanche, le binary log n’est pas un audit trail de sécurité complet : il ne remplace pas l’audit des connexions, des lectures SELECT ou des décisions d’autorisation.*

__*Mis à jour le 16/06/2026*__
