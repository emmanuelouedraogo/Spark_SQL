#### Pourquoi Spark SQL?

les fichiers prendent plus de volume dans la mémoire vive.
Pour éviter cette situation, l'objectif du calcul parallèle est de dispatcher les données sur plusieurs serveurs au sein d'un cluster pour profiter de la mémoire vive disponible sur plusieurs machines.
Il y a une tolérence à l'érreur grace au sytème de relais des autres serveurs.

Les Frameworks bigdata. hadoop et spark permettent de gérer.
hadoop est en java
spark de la même maison accepte python, R, scala, java ... qui est visiblement complémentaire à hadoop.
Spark se repose sur hadoop pour faire la gestions des serveurs dans un cluster.

#### Spark SQL en parallèle

Pour comprendre comment spark fonctionne sur plusieurs serveurs, examinez le tableau suivant :

```
|UserIB  | Date               | Event           | ProductID   |
 -------- -------------------- ----------------- -------------
|  0     | 2021-01-12T12:08:01|     view        |  576589     |
|  0     | 2021-01-12T12:08:08|     view        |  733961     |
|  1     | 2021-01-12T12:08:12|     purchase    |  987872     |
```

La comptabilisation du nombre d'évènements par utilisateurs se fait par regroupements.

### Parallélisation de calcul avec des lignes dépendantes entre-elles?

-**Découpage** de la table en plusieurs blocs, chaque bloque étant envoyé dans une machine.
-**Le combiner**:Toutes les machines regroupent les blocs selon les colonnes spécifiées
-**Le shuffling**:Toutes les valeurs associées aux colonnes à regrouper sont concatenées ensembles.

- **Agrégation**: Elle est réalisé directement sur la tables des valeurs concaténées.
Spark SQL ou Pandas ouien dplyr
> data\
> .groupby("UserID")\
> .agg(
    func.count("Event").alias("Num Events")
    ) 

OUTPUT:
```
|UserID| Num Events|
--------------------
|  0   |    2      |
--------------------
|  1   |    2      |
--------------------
|  2   |    2      |
--------------------
|  3   |    1      |
```

