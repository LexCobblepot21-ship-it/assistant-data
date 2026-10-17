# Databricks peut-il aider ce projet ?

*Produit le 17/10/2026 dans le projet « Créer un Assistant Data ».*

**Réponse courte** : oui, mais seulement si l'entreprise utilise déjà Databricks. Sinon, ce n'est pas le bon moment.

## Pourquoi

Databricks n'est pas un simple assistant qu'on ajoute au projet. C'est une plateforme de données complète dans le cloud, qui remplacerait le datawarehouse cible. Cela veut dire copier les données d'assurance dans le cloud, ce qui va beaucoup plus loin que la règle actuelle (« seules les métadonnées vont à l'IA »). C'est donc une décision de la DSI, pas un outil à tester seul.

## Ce qu'il apporterait, s'il est déjà là

- **Text-to-SQL (chantier B)** : c'est son point fort. Genie (aujourd'hui Genie One et Genie Agents) répond en langage naturel à partir des descriptions de tables et colonnes rangées dans Unity Catalog, plus des exemples de requêtes validées. C'est exactement le dictionnaire Cleva.
  [Doc Genie](https://docs.databricks.com/gcp/en/genie/) · [Ce que Genie attend comme contexte](https://atlan.com/know/ai-agent/databricks/databricks-genie-context-requirements/)
- **Migration (chantier A)** : l'outil gratuit [Lakebridge](https://www.databricks.com/blog/introducing-lakebridge-free-open-data-migration-databricks-sql) sait *analyser* du code SAS pour en mesurer le volume. D'après les recherches, sa *conversion* automatique ne couvre pas SAS (Oracle, Teradata, SQL Server… oui). Les macros et formats SAS resteraient donc à traduire avec notre méthode.
  [Détail par composant](https://kanerika.com/blogs/databricks-lakebridge/)
- **KNIME reste utilisable** : KNIME sait se connecter à Databricks. Les deux ne s'excluent pas.
  [Guide KNIME–Databricks](https://docs.knime.com/latest/databricks_integration_user_guide)

## Coûts

Paiement à la consommation (calcul et cloud), plus un abonnement cloud (Azure, AWS ou GCP). Genie One est gratuit pour les utilisateurs jusqu'au 31 janvier 2027, mais l'entrepôt SQL qui exécute les requêtes reste payant.

## Recommandation

On garde le plan actuel (SAS → SQL sur le DWH → KNIME, puis l'assistant avec le dictionnaire de données). Ce dictionnaire servira de toute façon, Databricks ou pas.

Question à poser à la DSI : « Avons-nous Databricks, ou est-ce prévu ? » Si oui, on revoit le chantier B autour de Genie.
