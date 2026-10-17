# Synthèse du document Word : stratégie de migration

*Produit le 16/10/2026 dans le projet « Créer un Assistant Data ».*

Ce Word donne un plan clair et réaliste. Voici l'essentiel.

## L'écart SAS / SQL

Le projet parle de migrer du « SQL », mais le document parle de requêtes **SAS** : des PROC SQL qui interrogent Oracle et contiennent des macros et des formats SAS. Le chemin est donc **SAS → SQL sur le datawarehouse → KNIME**.

## La stratégie

On ne réentraîne pas l'IA. On lui donne la documentation de tes bases, et elle s'appuie dessus. Le travail se fait en deux chantiers :

- **A. Migration** : on traduit les requêtes existantes. On commence par là, parce que le résultat peut être comparé à celui de SAS.
- **B. Text-to-SQL et rapports** : c'est plus risqué, car une requête peut sembler juste et donner un résultat faux. Ce chantier vient après A. On travaille en lecture seule sur le datawarehouse, et une personne relit chaque requête avant de l'exécuter.

## Les étapes

1. Faire valider par la DSI ce qu'on peut envoyer à l'IA. On n'envoie que des métadonnées, jamais de données de clients.
2. Construire le dictionnaire de données (tables, colonnes, sens métier, codes). Le schéma Cleva (f_prime, f_polices…) est un bon point de départ.
3. Documenter le passage d'Oracle vers le datawarehouse, colonne par colonne.
4. Réunir 5 à 10 requêtes SAS typiques avec leur résultat attendu.
5. Traduire ces requêtes en SQL pour le datawarehouse.
6. Les reproduire dans KNIME : d'abord avec un nœud DB Query Reader, puis avec des nœuds natifs.
7. Comparer les résultats de KNIME avec ceux de SAS, puis enchaîner sur le chantier B.

## Points ouverts

- L'accord de la DSI.
- L'existence de spécifications de l'ETL.
- La mise à jour de KNIME (version actuelle 4.7.8, alors que la 5.x intègre un assistant IA).

## Ce que ça implique pour l'assistant

Ses « connaissances » tiennent dans deux fichiers, **le dictionnaire de données** et **la correspondance Oracle → datawarehouse**, plus une série de requêtes déjà validées qui lui servent d'exemples. Ces mêmes fichiers serviront aussi pour le text-to-SQL. Il n'y a donc qu'un seul socle à construire pour les deux objectifs.

## Prochaine étape conseillée

Un essai complet sur une vraie requête SAS, par exemple celle sur les primes, en retirant toute donnée sensible.

## Liens utiles

- [Documentation KNIME](https://docs.knime.com/)
- [Guide des nœuds base de données KNIME](https://docs.knime.com/latest/db_extension_guide/index.html)
- [KNIME Hub (exemples)](https://hub.knime.com/)
