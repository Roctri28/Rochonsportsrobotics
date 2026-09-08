> ⚠️ **Document d'étude.** La voie retenue est la passerelle décrite dans
> [00-orientation.md](00-orientation.md), pas le remplacement d'Avantage.

# 1. Faisabilité

## Réponse courte

**Oui, c'est faisable — mais le logiciel n'est pas la partie difficile.**

Un grand livre, des comptes fournisseurs, un module de facturation : c'est de la mécanique
connue, quelques mois de développement. Ce qui rend un « Avantage » difficile à remplacer,
c'est trois choses qui n'ont presque rien à voir avec le code :

1. **Le référentiel des conventions collectives.** Quatre secteurs (résidentiel,
   institutionnel/commercial, industriel, génie civil et voirie), des dizaines de métiers et
   d'occupations, des taux qui changent à chaque révision de convention, des primes, des
   règles d'heures supplémentaires, des indemnités de déplacement et de séjour, des ratios
   compagnon/apprenti. Ce n'est pas un développement : c'est un **abonnement à un travail de
   veille permanent**. Un éditeur établi vend d'abord cela.
2. **La transmission vers la CCQ.** Le rapport mensuel doit sortir dans un format accepté
   par la CCQ. Il faut obtenir les spécifications techniques de transmission de fichier et,
   selon le cas, passer par un processus de validation/homologation fournisseur. **À
   confirmer directement auprès du service aux employeurs de la CCQ avant de chiffrer quoi
   que ce soit** — c'est le seul point qui peut bloquer le projet.
3. **La responsabilité.** Une erreur de paie construction ne se corrige pas par un correctif
   logiciel : elle produit des arrérages, des plaintes, des pénalités et des vérifications.
   Le niveau de preuve exigé avant de mettre le système en production est celui d'un système
   bancaire, pas celui d'une application de gestion.

## Ce que l'IA change réellement

L'IA n'accélère **pas** le calcul de la paie : il est déjà instantané dans les logiciels
existants. Elle accélère ce qui prend réellement du temps chez un entrepreneur :

- ressaisir des feuilles de temps papier ou des photos venues du chantier ;
- ventiler des factures fournisseurs au bon chantier et au bon code de coût ;
- chercher « quelle prime s'applique dans ce cas » dans une convention collective ;
- repérer les anomalies d'un rapport mensuel **avant** de le transmettre plutôt qu'après une
  vérification de la CCQ.

C'est là qu'un facteur 3 à 5 sur le temps administratif est plausible. Le reste du gain
annoncé par les produits « IA » du marché est marketing.

## Ordre de grandeur

| Objectif | Effort réaliste |
|---|---|
| Outil interne GTR : paie + rapport mensuel CCQ + coût de revient | 6 à 12 mois, équipe de 2 à 4 personnes |
| Produit commercialisable, multi-entrepreneurs, multi-secteurs | 2 à 3 ans + une fonction de veille conventions à temps plein |
| Maintien annuel du référentiel conventions (récurrent, incompressible) | 0,3 à 0,5 ETP |

## Les questions à trancher avant de commencer

1. La CCQ accepte-t-elle des fichiers d'un logiciel tiers non homologué, et à quelles
   conditions ? (question bloquante)
2. Le but est-il un outil interne pour GTR, ou un produit à vendre ? Les deux ne se
   construisent pas pareil.
3. Dans quels secteurs et régions GTR opère-t-il, et combien de salariés assujettis ?
   Cela détermine la taille du référentiel à construire.
4. Peut-on extraire l'historique d'Avantage (dossiers employés, cumuls année à date,
   historique de paie) dans un format exploitable ? Sans cela, la bascule est très coûteuse.
5. Qui porte la responsabilité professionnelle et avec quelle assurance ?
