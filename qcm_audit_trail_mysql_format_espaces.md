  **Partie 1**  
    **Question 1 : Dans une stratégie d'audit trail MySQL basée sur des triggers, quelles affirmations sont techniquement correctes pour tracer les modifications d'une table métier InnoDB ?**  
Lien d'aide : https://dev.mysql.com/doc/refman/8.4/en/create-trigger.html  
*A. Un trigger AFTER UPDATE peut lire OLD.colonne et NEW.colonne pour enregistrer l'ancienne et la nouvelle valeur dans une table d'audit.*
*B. Un trigger BEFORE UPDATE peut exécuter COMMIT pour garantir que la ligne d'audit soit persistée même si la transaction métier est annulée.*
*C. Un trigger peut écrire dans une table d'audit distincte, mais ne doit pas modifier directement la même table que celle qui l'a déclenché.*
*D. Une table d'audit peut stocker l'identifiant métier, l'opération, l'utilisateur SQL, l'horodatage, OLD et NEW sous forme de colonnes ou de JSON.*
*E. Les triggers sont adaptés pour tracer les INSERT, UPDATE et DELETE, mais ils ne permettent pas de tracer directement les SELECT.*
    **Question 2 : Concernant MySQL Enterprise Audit, quelles affirmations sont exactes pour construire un audit trail technique au niveau serveur ?**  
Lien d'aide : https://dev.mysql.com/doc/refman/8.4/en/audit-log-filtering.html  
*A. MySQL Enterprise Audit permet de filtrer les événements audités au moyen de règles et de les associer à des comptes utilisateurs.*
*B. MySQL Enterprise Audit est une fonctionnalité disponible nativement dans MySQL Community Edition sans composant supplémentaire.*
*C. Le filtrage avancé nécessite que le plugin d'audit, les tables d'audit et les fonctions associées soient installés.*
*D. MySQL Enterprise Audit peut aider à tracer des événements de connexion, d'activité SQL et d'accès serveur, mais ne remplace pas toujours un audit fonctionnel ligne par ligne avec OLD et NEW.*
*E. Les règles d'audit doivent forcément être écrites dans le fichier my.cnf et ne peuvent pas être gérées via des fonctions SQL.*
    **Question 3 : Si l'on utilise le binary log comme source complémentaire d'audit trail dans MySQL, quelles affirmations sont techniquement correctes ?**  
Lien d'aide : https://dev.mysql.com/doc/refman/8.4/en/binary-log-formats.html  
*A. Avec le format ROW, le binary log enregistre les événements décrivant les lignes affectées par les changements de données.*
*B. Le binary log est suffisant pour auditer tous les SELECT exécutés par les utilisateurs applicatifs.*
*C. Le binary log est principalement conçu pour la réplication et la restauration à un instant donné, mais peut aussi servir de source technique pour analyser des changements.*
*D. Le format STATEMENT peut poser des problèmes avec certaines instructions non déterministes, ce qui rend le format ROW plus robuste pour reconstruire les changements de lignes.*
*E. Une stratégie d'audit sérieuse doit gérer la rétention, la protection et l'accès aux fichiers binlog si ceux-ci sont utilisés comme preuve technique.*
  **Partie 2**  
Question 1  
Réponse : A, C, D, E  
*Explication : Les triggers MySQL permettent d'utiliser OLD et NEW pour capturer les valeurs avant et après modification, puis d'insérer une trace dans une table d'audit séparée. Ils sont utiles pour les INSERT, UPDATE et DELETE, mais ne tracent pas les SELECT. Un trigger ne doit pas modifier la table qui l'a déclenché, et il ne peut pas sécuriser une écriture d'audit au moyen d'un COMMIT autonome dans la transaction métier.*
Question 2  
Réponse : A, C, D  
*Explication : MySQL Enterprise Audit est une fonctionnalité de l'édition Enterprise permettant de produire un journal d'audit serveur avec des règles de filtrage. Pour le filtrage avancé, il faut installer le plugin, les tables et les fonctions associées. Cette approche trace des événements serveur, mais elle ne remplace pas toujours un audit fonctionnel détaillé dans des tables métier avec OLD et NEW.*
Question 3  
Réponse : A, C, D, E  
*Explication : Le binary log est conçu pour la réplication et la restauration à un instant donné, mais il peut compléter un audit trail en fournissant une trace technique des changements. Le format ROW décrit les lignes affectées, alors que le format STATEMENT peut être moins fiable avec des instructions non déterministes. En revanche, le binary log ne capture pas tous les SELECT et doit être protégé, conservé et exploité avec une politique claire.*

*Sous licence CC BY - Mise à jour le 16/06/2026*
