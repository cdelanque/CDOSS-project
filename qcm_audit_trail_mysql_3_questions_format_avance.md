**Partie 1**  
  **Question 1 : Dans MySQL Enterprise Audit, quelles affirmations sont techniquement correctes pour obtenir un audit trail filtré par utilisateur ou par règle ?**
  Lien d’aide : https://dev.mysql.com/doc/refman/8.4/en/audit-log-filtering.html  
*A. Il faut que le plugin audit log soit installé avec les tables et fonctions nécessaires au filtrage par règles.*  
*B. Après installation du filtrage par règles, tous les événements auditables sont journalisés par défaut pour tous les utilisateurs.*  
*C. Une règle de filtrage peut être définie avec une fonction SQL comme audit_log_filter_set_filter().*  
*D. Une règle de filtrage peut être affectée à un compte avec une fonction SQL comme audit_log_filter_set_user().*  
*E. MySQL Community Edition fournit nativement le même plugin MySQL Enterprise Audit que MySQL Enterprise Edition.*  
  **Question 2 : Dans une stratégie d’audit trail basée sur des triggers MySQL, quelles affirmations sont exactes concernant les pseudo-enregistrements OLD et NEW et le comportement transactionnel ?**
  Lien d’aide : https://dev.mysql.com/doc/refman/en/trigger-syntax.html  
*A. Un trigger AFTER INSERT, AFTER UPDATE ou AFTER DELETE peut écrire une ligne dans une table d’audit pour chaque ligne métier modifiée.*  
*B. Dans un trigger INSERT, il est possible d’utiliser simultanément OLD.colonne et NEW.colonne pour comparer l’ancien et le nouveau contenu.*  
*C. Dans un trigger UPDATE, OLD.colonne permet de lire la valeur avant modification et NEW.colonne permet de lire la valeur après modification.*  
*D. Un trigger peut exécuter explicitement COMMIT afin de conserver l’audit même si la transaction métier est ensuite annulée.*  
*E. Pour les tables transactionnelles, l’échec du trigger provoque l’échec de l’instruction déclenchante et la restauration des changements de cette instruction.*  
  **Question 3 : Dans une architecture d’audit trail MySQL combinant tables d’audit applicatives et binary log, quelles affirmations sont correctes ?**
  Lien d’aide : https://dev.mysql.com/doc/refman/8.4/en/binary-log-formats.html  
*A. En format ROW, le binary log enregistre des événements décrivant les lignes affectées par les modifications.*  
*B. Le format STATEMENT est toujours sûr pour auditer des traitements non déterministes, car il garantit que la source et la réplique obtiendront les mêmes lignes modifiées.*  
*C. Même avec le format ROW, certaines opérations comme les DDL peuvent être écrites sous forme d’instructions dans le binary log.*  
*D. Le binary log remplace totalement une table d’audit métier, car il contient naturellement le motif fonctionnel de la modification et le contexte applicatif complet.*  
*E. Le binary log peut compléter un audit trail en aidant à reconstruire des modifications techniques et à alimenter des scénarios de réplication ou de reprise.*  
**Partie 2**  
Question 1  
Réponse : A, C, D  
  *Explication : Le filtrage MySQL Enterprise Audit repose sur le plugin audit log et sur les objets SQL associés au filtrage par règles. Les filtres peuvent être définis avec audit_log_filter_set_filter() puis affectés à des comptes avec audit_log_filter_set_user(). Le comportement par défaut du filtrage par règles ne consiste pas à tout journaliser automatiquement, et le plugin Enterprise Audit n’est pas une fonctionnalité native équivalente de MySQL Community Edition.*
Question 2  
Réponse : A, C, E  
  *Explication : Les triggers sont exécutés pour chaque ligne affectée et peuvent écrire dans une table d’audit. OLD et NEW dépendent du type d’événement : INSERT ne fournit que NEW, DELETE ne fournit que OLD, et UPDATE fournit OLD et NEW. Les triggers ne peuvent pas exécuter explicitement COMMIT ou ROLLBACK ; pour les tables transactionnelles, une erreur dans le trigger fait échouer l’instruction déclenchante et entraîne la restauration des modifications associées.*
Question 3  
Réponse : A, C, E  
  *Explication : Le binary log peut être utilisé comme source technique complémentaire, notamment avec le format ROW qui décrit les lignes modifiées. Il ne remplace pas un audit trail métier, car il ne contient pas nécessairement le motif fonctionnel, le ticket, l’écran applicatif ou le contexte métier complet. Le format STATEMENT peut poser problème avec des instructions non déterministes ; le format ROW est donc généralement plus adapté pour reconstruire précisément les changements de données.*

*Sous licence CC BY - Mise à jour le 16/06/2026*
