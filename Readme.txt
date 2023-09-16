Pourquoi Spark SQL?
les fichiers prendent plus de volume dans la mémoire vive.
Pour éviter cette situation, l'objectif du calcul parallèle est de dispatcher les données sur plusieurs serveurs au sein d'un cluster pour profiter de la mémoire vive disponible sur plusieurs machines.
Il y a une tolérence à l'érreur grace au sytème de relais des autres serveurs.

Les Frameworks bigdata. hadoop et spark permettent de gérer.
hadoop est en java 
spark de la même maison accepte python, R, scala, java ... qui est visiblement complémentaire à hadoop.
Spark se repose sur hadoop pour faire la gestions des serveurs dans un cluster.

#### Spark SQL en parallèle #####

To understand how spark operates on multiple servers, consider the following table:

|UserIB  | Date               | Event           | ProductID   |
 -------- -------------------- ----------------- -------------
|  0     | 2021-01-12T12:08:01|     view        |  576589     |
|  0     | 2021-01-12T12:08:08|     view        |  733961     |
|  1     | 2021-01-12T12:08:12|     purchase    |  987872     |


