**Partie 1**  
  **Question 1 : Dans MySQL Enterprise Audit, quelles affirmations sont techniquement correctes pour activer un audit trail filtré capable de journaliser les connexions et les requêtes sensibles ?**  
Aide : https://dev.mysql.com/doc/refman/8.4/en/audit-log-filtering.html  
*A. Il faut installer le composant ou plugin Enterprise Audit avant d'utiliser les fonctions de filtrage d'audit.*  
*B. Par défaut, le filtrage par règles journalise automatiquement tous les événements de tous les utilisateurs.*  
*C. Un filtre peut être défini avec audit_log_filter_set_filter() puis affecté à un compte avec audit_log_filter_set_user().*  
*D. La variable audit_log_filter_id permet d'indiquer le filtre affecté à la session courante, mais elle est en lecture seule.*  
*E. Les définitions de filtres peuvent être consultées dans une table système telle que mysql.audit_log_filter.*  
  **Question 2 : Pour construire un audit trail applicatif à base de triggers sur une table InnoDB sensible, quelles affirmations décrivent correctement l'utilisation de OLD, NEW et des événements de trigger MySQL ?**  
Aide : https://dev.mysql.com/doc/refman/8.4/en/trigger-syntax.html  
*A. Dans un trigger INSERT, on peut lire NEW.colonne, mais pas OLD.colonne.*  
*B. Dans un trigger DELETE, on peut lire OLD.colonne, mais pas NEW.colonne.*  
*C. Dans un trigger UPDATE, OLD.colonne désigne la valeur avant modification et NEW.colonne la valeur après modification.*  
*D. Un même trigger MySQL peut être défini simultanément sur INSERT, UPDATE et DELETE avec une seule instruction CREATE TRIGGER.*  
*E. Un trigger FOR EACH ROW peut alimenter une table d'audit contenant l'opération, l'identifiant métier, les anciennes valeurs, les nouvelles valeurs et l'horodatage.*  
  **Question 3 : Dans une stratégie d'audit trail MySQL reposant partiellement sur le binary log, quelles affirmations sont exactes concernant l'exploitation technique des événements de lignes ?**  
Aide : https://dev.mysql.com/doc/refman/8.4/en/mysqlbinlog-row-events.html  
*A. Avec le row-based binary logging, les opérations INSERT, UPDATE et DELETE sont représentées par des événements de lignes tels que WRITE_ROWS_EVENT, UPDATE_ROWS_EVENT et DELETE_ROWS_EVENT.*  
*B. L'outil mysqlbinlog peut afficher des événements de lignes avec les options --base64-output=DECODE-ROWS et --verbose.*  
*C. Le binary log suffit toujours à connaître l'utilisateur applicatif métier à l'origine d'une modification, même si toutes les connexions passent par un compte technique unique.*  
*D. Le binary log peut être utile pour reconstruire des modifications de données, mais il ne remplace pas forcément une table d'audit métier enrichie avec un contexte applicatif.*  
*E. Si le binary log est désactivé, certaines stratégies de réplication et de restauration point-in-time deviennent impossibles ou fortement limitées.*  
**Partie 2**  

Réponse Q1 : A, C, D et E  
  *Explication : Enterprise Audit est une fonctionnalité de MySQL Enterprise qui doit être installée avant l'utilisation opérationnelle de ses filtres. Les filtres peuvent être créés avec audit_log_filter_set_filter(), associés avec audit_log_filter_set_user(), et consultés dans les tables de filtre. Le point B est faux, car le filtrage par règles ne journalise pas automatiquement tous les événements par défaut.*
Réponse Q2 : A, B, C et E  
  *Explication : MySQL expose NEW dans les triggers INSERT, OLD dans les triggers DELETE, et les deux dans les triggers UPDATE. Un trigger est associé à un seul événement INSERT, UPDATE ou DELETE ; il faut donc plusieurs triggers pour couvrir les trois opérations. Une table d'audit peut être alimentée ligne par ligne avec l'opération, les valeurs avant/après, l'horodatage et d'autres métadonnées.*
Réponse Q3 : A, B, D et E  
  *Explication : En journalisation par lignes, MySQL encode les modifications sous forme d'événements WRITE_ROWS, UPDATE_ROWS et DELETE_ROWS, que mysqlbinlog peut rendre plus lisibles avec les options adaptées. Le binary log aide à reconstruire des modifications et soutient la réplication ou la restauration point-in-time, mais il ne contient pas toujours le contexte métier complet, notamment si l'application utilise un compte technique partagé.*

*Sous licence CC BY - Mise à jour le 16/06/2026*
