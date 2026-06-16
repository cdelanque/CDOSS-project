**Partie 1**  
  **Question 1 : Dans Azure Cosmos DB for MongoDB, quelles affirmations décrivent correctement le modèle technique du service par rapport à une base MongoDB native auto-hébergée ?**  
Lien d'aide : [Introduction à Azure Cosmos DB for MongoDB](https://learn.microsoft.com/fr-fr/azure/cosmos-db/mongodb/introduction)  
*A. Azure Cosmos DB for MongoDB permet d'utiliser des pilotes clients MongoDB existants grâce à la compatibilité avec le protocole filaire MongoDB.*  
*B. Azure Cosmos DB for MongoDB correspond à une instance MongoDB Community ou Enterprise installée et administrée manuellement par le client sur une VM Azure.*  
*C. Azure Cosmos DB for MongoDB apporte des capacités managées Azure comme la distribution mondiale, le partitionnement automatique, les sauvegardes et le chiffrement au repos.*  
*D. Toutes les commandes d'administration bas niveau de MongoDB Enterprise sont obligatoirement disponibles, sans restriction, car le service exécute le moteur MongoDB officiel.*  
*E. L'utilisation du service peut nécessiter de vérifier les différences de comportement et de compatibilité avant une migration lift-and-shift depuis une base MongoDB existante.*  
  **Question 2 : Lors de la conception d'une collection Azure Cosmos DB for MongoDB partitionnée, quelles décisions techniques sont critiques pour limiter les partitions chaudes et les requêtes cross-partition coûteuses ?**  
Lien d'aide : [Partitionnement et mise à l'échelle horizontale dans Azure Cosmos DB](https://learn.microsoft.com/fr-fr/azure/cosmos-db/partitioning)  
*A. Choisir une clé de partition à forte cardinalité afin de répartir les données et la consommation de RU sur plusieurs partitions logiques.*  
*B. Choisir une clé de partition alignée avec les filtres d'égalité les plus fréquents des requêtes de lecture importantes.*  
*C. Choisir une clé de partition dont la valeur change régulièrement afin que les documents puissent être redistribués automatiquement selon la charge.*  
*D. Ignorer la clé de partition lorsque la collection peut croître fortement, car Azure Cosmos DB corrige toujours automatiquement les mauvais choix de modélisation sans migration.*  
*E. Surveiller les risques de partitions chaudes, car une mauvaise distribution de la charge peut provoquer du throttling et augmenter les coûts.*  
  **Question 3 : Pour optimiser les requêtes MongoDB sur Azure Cosmos DB for MongoDB, quelles affirmations sont correctes concernant les index et les fonctionnalités compatibles ?**  
Lien d'aide : [Gérer l'indexation dans Azure Cosmos DB for MongoDB](https://learn.microsoft.com/fr-fr/azure/cosmos-db/mongodb/indexing)  
*A. Pour les versions serveur 3.6 et ultérieures, Azure Cosmos DB for MongoDB indexe automatiquement le champ _id et la clé de partition dans les collections partitionnées.*  
*B. Les index composés peuvent être nécessaires pour optimiser certaines requêtes filtrant ou triant sur plusieurs champs.*  
*C. Les index inutiles ou mal alignés avec les requêtes peuvent augmenter le coût des écritures, car ils doivent être maintenus lors des insertions et mises à jour.*  
*D. Il est toujours inutile de créer des index manuellement, car Azure Cosmos DB for MongoDB crée automatiquement tous les index nécessaires à toutes les requêtes.*  
*E. Avant de migrer une application MongoDB existante, il faut vérifier les fonctionnalités et comportements supportés, car la compatibilité n'implique pas que toutes les commandes et options MongoDB soient identiques.*  
**Partie 2**  
Réponse Q1 : A, C et E.  
*Explication : Azure Cosmos DB for MongoDB expose une compatibilité avec les pilotes MongoDB via le protocole filaire, mais ce n'est pas une VM Azure sur laquelle le client administre lui-même MongoDB Community ou Enterprise. Le service ajoute des capacités managées Azure, comme le partitionnement, la distribution globale, la sécurité, les sauvegardes et l'intégration avec Azure. Une migration depuis MongoDB natif doit donc vérifier les compatibilités et différences de comportement.*
Réponse Q2 : A, B et E.  
*Explication : Le choix de la clé de partition est une décision majeure. Une bonne clé possède une forte cardinalité, répartit correctement les données et les RU, et correspond aux principaux filtres de requêtes afin d'éviter des lectures cross-partition inutiles. Une clé de partition n'est pas conçue pour changer régulièrement et un mauvais choix peut produire des partitions chaudes, du throttling et des coûts plus élevés.*
Réponse Q3 : A, B, C et E.  
*Explication : Azure Cosmos DB for MongoDB indexe automatiquement certains champs essentiels comme _id et la clé de partition, mais cela ne remplace pas l'analyse des requêtes métier. Les index composés peuvent être nécessaires pour les filtres et tris multi-champs. Chaque index a un coût de maintenance en écriture. Enfin, la compatibilité MongoDB doit être validée précisément avant migration, notamment pour les commandes, options et comportements avancés.*

*Sous licence CC BY - Mise à jour le 16/06/2026*
