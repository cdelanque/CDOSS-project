**Partie 1**  

  **Question 1 : Dans MySQL Enterprise Audit, quelles affirmations sont techniquement correctes concernant la mise en place d’un audit trail filtré par utilisateur, type d’événement et règle JSON ?**  
Lien d’aide : [MySQL Enterprise Audit - Audit Log Filtering](https://dev.mysql.com/doc/refman/8.4/en/audit-log-filtering.html)  
*A. Le filtrage par règles nécessite que le plugin Enterprise Audit, les tables d’audit et les fonctions associées soient installés.*  
*B. Par défaut, le filtrage par règles journalise automatiquement tous les événements auditables pour tous les utilisateurs.*  
*C. Une règle peut être affectée à un compte utilisateur précis ou au compte générique %, utilisé comme filtre par défaut.*  
*D. Un filtre peut inclure ou exclure des événements selon la classe, la sous-classe, l’utilisateur ou certains champs de l’événement.*  
*E. MySQL Community Server fournit nativement le même plugin Enterprise Audit que MySQL Enterprise Edition.*  

  **Question 2 : Lorsqu’un audit trail est construit avec des triggers MySQL sur une table métier InnoDB, quelles affirmations sont correctes pour tracer les modifications de données ?**  
Lien d’aide : [MySQL Trigger Syntax and Examples](https://dev.mysql.com/doc/refman/en/trigger-syntax.html)  
*A. Dans un trigger UPDATE, OLD permet de lire l’état avant modification et NEW permet de lire l’état après modification.*  
*B. Dans un trigger DELETE, NEW contient la ligne supprimée et permet d’enregistrer l’image supprimée dans la table d’audit.*  
*C. Dans un trigger INSERT, OLD permet d’identifier l’état de la ligne avant insertion.*  
*D. Plusieurs triggers peuvent exister pour le même événement et le même moment d’exécution, avec un ordre contrôlé par FOLLOWS ou PRECEDES.*  
*E. Les triggers permettent de tracer les INSERT, UPDATE et DELETE réussis, mais ne suffisent pas à auditer les SELECT, les connexions ou les commandes d’administration.*  

  **Question 3 : Si l’on utilise le binary log MySQL comme source complémentaire d’audit technique, quelles affirmations sont correctes ?**  
Lien d’aide : [MySQL Binary Log](https://dev.mysql.com/doc/mysql/en/binary-log.html)  
*A. Le binary log contient des événements décrivant des changements de données ou de structure, et sert notamment à la réplication et à la restauration point-in-time.*  
*B. Le binary log enregistre aussi les SELECT et SHOW qui ne modifient aucune donnée.*  
*C. En format ROW, le binary log permet d’observer des événements de modification ligne par ligne, mais il ne remplace pas un audit trail métier enrichi avec utilisateur applicatif, motif et contexte fonctionnel.*  
*D. La désactivation du binary log n’a aucun impact sur la restauration incrémentale après sauvegarde complète.*  
*E. Les fichiers de binary log et relay log peuvent contenir des informations sensibles et doivent être protégés, éventuellement par chiffrement lorsque l’option est activée.*  

**Partie 2**  

Question 1  
Réponse : A, C et D.  
*Explication : Le filtrage Enterprise Audit repose sur le plugin, les tables et les fonctions d’audit. Les filtres peuvent être définis par règles, affectés à des comptes précis ou au compte %, et sélectionner les événements selon plusieurs caractéristiques. En revanche, le filtrage par règles ne journalise pas tout par défaut et le plugin Enterprise Audit relève de MySQL Enterprise, pas de MySQL Community.*  

Question 2  
Réponse : A, D et E.  
*Explication : Pour UPDATE, OLD représente l’ancienne image et NEW la nouvelle image. MySQL autorise plusieurs triggers de même événement et de même moment d’exécution avec un ordre explicite. Un audit par triggers est utile pour les changements DML réussis, mais il ne couvre pas naturellement les lectures SELECT, les connexions, les échecs d’authentification ou les opérations d’administration.*  

Question 3  
Réponse : A, C et E.  
*Explication : Le binary log est une source technique précieuse pour la réplication et la restauration point-in-time, et le format ROW peut aider à analyser les modifications ligne par ligne. Cependant, il ne journalise pas les lectures sans modification, ne remplace pas un audit trail métier contextualisé, et ses fichiers doivent être protégés car ils peuvent contenir des informations sensibles.*  

*Sous licence CC BY - Mise à jour le 16/06/2026*
