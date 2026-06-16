**Partie 1**  
**Question 1 : Dans MySQL Enterprise, quels éléments sont nécessaires ou pertinents pour mettre en place un audit trail natif avec filtrage fin des événements ?**
Lien : https://dev.mysql.com/doc/refman/8.4/en/audit-log-filtering.html
*A. Installer MySQL Enterprise Audit avec les tables et fonctions nécessaires au filtrage par règles.*  
*B. Définir des règles de filtrage avec des fonctions comme audit_log_filter_set_filter(), puis les associer à des comptes avec audit_log_filter_set_user().*  
*C. Utiliser uniquement le binary log, car il journalise automatiquement les SELECT, les connexions refusées et tous les événements d’authentification.*  
*D. Prévoir que l’audit log Enterprise est une fonctionnalité de MySQL Enterprise Edition, et non une fonctionnalité native complète de MySQL Community Edition.*  
*E. Créer un trigger AFTER SELECT sur les tables sensibles afin de tracer toutes les lectures de données confidentielles.*  
**Question 2 : Dans MySQL Community, si l’on construit un audit trail applicatif avec des triggers, quelles affirmations sont techniquement correctes ?**
Lien : https://dev.mysql.com/doc/refman/8.4/en/triggers.html
*A. Des triggers AFTER INSERT, AFTER UPDATE et AFTER DELETE peuvent insérer dans une table d’audit les anciennes et nouvelles valeurs des lignes modifiées.*  
*B. Dans un trigger UPDATE, les pseudo-enregistrements OLD et NEW permettent de comparer l’état avant et après modification.*  
*C. Un trigger MySQL peut être défini sur SELECT pour tracer automatiquement les lectures de lignes sensibles.*  
*D. Les triggers d’audit doivent être conçus pour éviter les boucles, les effets de bord et les droits excessifs sur les tables d’audit.*  
*E. Les triggers de table capturent automatiquement les changements DDL, les échecs de connexion et les commandes d’administration serveur.*  
**Question 3 : Pour un audit trail MySQL robuste, comment distinguer les rôles du binary log, du general query log et d’un vrai mécanisme d’audit ?**
Lien : https://dev.mysql.com/doc/mysql/en/binary-log.html
*A. Le binary log enregistre des événements décrivant les changements de données et sert notamment à la réplication et à la récupération point-in-time.*  
*B. Le binary log ne constitue pas à lui seul un audit trail fonctionnel complet, car il ne journalise pas les SELECT et ne couvre pas tous les événements de sécurité.*  
*C. Le general query log peut aider à diagnostiquer ou tracer des requêtes, mais il peut devenir volumineux et ne remplace pas une stratégie d’audit sécurisée et maîtrisée.*  
*D. Un audit trail conforme doit donner aux comptes applicatifs le droit DELETE sur les tables d’audit pour faciliter la purge manuelle.*  
*E. Une architecture robuste peut combiner audit natif, triggers ciblés, binary logs pour la reprise, et export vers un stockage externe protégé contre l’altération.*  
**Partie 2**  
Question 1
Réponse : A, B, D  
*Explication : MySQL Enterprise Audit permet de journaliser des événements via un mécanisme d’audit natif et de filtrer les événements grâce à des règles et à des fonctions dédiées. Cette approche nécessite les composants, tables et fonctions d’audit appropriés. Le binary log n’est pas suffisant pour auditer toutes les actions de sécurité, et MySQL ne fournit pas de trigger SELECT pour auditer les lectures de tables.*
Question 2
Réponse : A, B, D  
*Explication : En MySQL Community, une solution fréquente consiste à créer des tables d’audit et des triggers ligne à ligne sur INSERT, UPDATE et DELETE. OLD et NEW permettent de capturer les anciennes et nouvelles valeurs selon le type d’opération. En revanche, les triggers MySQL ne s’appliquent pas aux SELECT et ne couvrent pas automatiquement les événements serveur comme les connexions échouées ou les changements DDL.*
Question 3
Réponse : A, B, C, E  
*Explication : Le binary log est essentiel pour la réplication et la récupération point-in-time, mais il n’est pas conçu comme un journal d’audit complet des accès et événements de sécurité. Le general query log peut tracer davantage de requêtes, mais il doit être utilisé avec prudence à cause du volume et des impacts opérationnels. Une stratégie sérieuse combine plusieurs mécanismes et protège les journaux contre la modification ou la suppression non autorisée.*

*Sous licence CC BY - Mise à jour le 16/06/2026*
