# 3. Architecture proposée

## 3.1 Principe directeur

> Les conventions collectives sont des **données versionnées**, jamais du code.

Chaque taux, prime, ratio et règle est une ligne de référentiel portant une **date d'effet**,
un secteur, un métier, une région. Chaque paie calculée enregistre l'identifiant de la
version de référentiel utilisée. Conséquences :

- une révision de convention est une mise à jour de données, pas un déploiement ;
- un recalcul rétroactif est reproductible à l'identique ;
- une vérification CCQ se répond en montrant la règle appliquée et sa source.

## 3.2 Modèle de données — points sensibles

- **Paie immuable.** Une paie émise ne se modifie pas ; on émet un ajustement lié. Journal
  d'écritures en ajout seul (append-only) pour la paie et le grand livre.
- **Temps bitemporel.** Distinguer la date d'effet (quand la règle s'applique) de la date
  de connaissance (quand on l'a enregistrée). Indispensable pour les rétroactifs de
  convention, qui sont fréquents.
- **Multi-tenant** dès le départ, même pour un client unique : cela évite une réécriture si
  le produit est commercialisé.
- **Journal d'audit intégral** : qui, quoi, quand, valeur avant/après, sur toute donnée de
  paie ou de conformité.

## 3.3 Pile technique suggérée

| Couche | Choix | Motif |
|---|---|---|
| Base de données | PostgreSQL | Transactionnel strict, contraintes, types `numeric` exacts, extensions temporelles |
| Backend | TypeScript (NestJS) ou Python (FastAPI) | Un seul langage partagé avec le frontend, ou l'écosystème data ; trancher selon l'équipe |
| Moteur de règles | Module déterministe maison, testé unitairement | Aucun moteur de règles générique : la traçabilité prime sur la souplesse |
| Frontend web | React + TypeScript | Bureau : paie, comptabilité, tableaux de bord |
| Saisie chantier | Application mobile avec mode hors-ligne | Le réseau n'est pas fiable en chantier ; la synchronisation différée est une exigence, pas une option |
| Couche IA | Service séparé, appelé en amont du noyau | L'IA produit des propositions ; le noyau ne l'appelle jamais pendant un calcul |
| Hébergement | Région canadienne, chiffrement au repos et en transit | Loi 25 (renseignements personnels) |

**Règle absolue sur les montants** : aucun calcul monétaire en virgule flottante. Entiers
en cents ou `numeric` en base, arrondi explicite et documenté à chaque étape.

## 3.4 Découpage en modules

```
noyau-referentiel     conventions, taux, primes, ratios, dates d'effet
noyau-paie            calcul déterministe, retenues, cumuls année à date
noyau-conformite      rapport mensuel CCQ, DAS, CNESST, T4/RL-1
chantier              projets, codes de coût, imputation, budget vs réel
facturation           facturation progressive, retenues contractuelles, comptes clients
fournisseurs          comptes fournisseurs, bons de commande, sous-traitance
comptabilite          grand livre, taxes, conciliation  (ou connecteur d'export)
ia-assistance         OCR, extraction, classification, détection d'anomalies, copilote
integrations          bancaire, système comptable existant, transmission CCQ
```

Les modules `ia-*` ne peuvent avoir aucune dépendance entrante depuis `noyau-*`. Cette
contrainte se vérifie automatiquement en intégration continue.

## 3.5 Sécurité et conformité

- Accès par rôle, séparation stricte des données de paie.
- Authentification à deux facteurs obligatoire sur les rôles paie et comptabilité.
- Conservation des registres sur la durée exigée par la CCQ et les autorités fiscales
  (durée exacte à confirmer, prévoir au minimum six ans).
- Sauvegardes chiffrées, restauration testée périodiquement.
- Aucune donnée nominative de paie envoyée à un fournisseur de modèle sans entente de
  traitement, sans engagement de non-entraînement et sans hébergement conforme.
