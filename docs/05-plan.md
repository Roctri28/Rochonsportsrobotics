> ⚠️ **Document d'étude.** La voie retenue est la passerelle décrite dans
> [00-orientation.md](00-orientation.md), pas le remplacement d'Avantage.

# 5. Plan de livraison

## Phase 0 — Découverte (2 à 4 semaines)

Objectif : lever les inconnues qui peuvent tuer le projet, avant d'écrire du code.

- [ ] Contacter la CCQ (service aux employeurs) : format et spécifications de transmission
      du rapport mensuel, conditions d'utilisation par un logiciel tiers, processus de
      validation éventuel. **Bloquant.**
- [ ] Vérifier la capacité d'extraction des données depuis le système actuel de GTR
      (dossiers salariés, historique de paie, cumuls année à date, chantiers, plan comptable).
- [ ] Cartographier le processus administratif réel de GTR, chronomètre à la main : combien
      d'heures par semaine sur la saisie de temps, sur les factures, sur le rapport mensuel.
      C'est la base de référence contre laquelle le gain sera mesuré.
- [ ] Établir le périmètre exact : secteurs, régions, métiers, nombre de salariés.
- [ ] Décider : outil interne ou produit commercialisable.

**Sortie** : décision continuer / arrêter, avec une estimation chiffrée.

## Phase 1 — Référentiel et moteur de paie (8 à 12 semaines)

- Modèle de données du référentiel de conventions, avec dates d'effet.
- Chargement des taux et règles pour le périmètre GTR uniquement.
- Moteur de calcul déterministe, couverture de tests unitaires élevée sur les règles.
- Import des dossiers salariés et de l'historique.

**Critère d'acceptation, non négociable** : rejouer **douze mois** de paies historiques de
GTR et obtenir un écart de **0,00 $** sur chaque salarié, chaque période, chaque retenue,
comparé au système actuel. Tant que ce test n'est pas vert, rien ne va en production.

## Phase 2 — Conformité (6 à 8 semaines)

- Génération du rapport mensuel CCQ, contrôles de validation, transmission.
- Retenues à la source, remises, CNESST.
- T4 et Relevé 1.
- Fonctionnement **en parallèle** du système actuel pendant au moins trois cycles complets
  de paie et un cycle de fin de mois. Aucune bascule sèche.

## Phase 3 — Saisie de temps et première IA (6 à 8 semaines)

- Application mobile de saisie en chantier, mode hors-ligne, synchronisation différée.
- Extraction assistée par IA des feuilles de temps papier et des fichiers de sous-traitants.
- Contrôles d'anomalies avant paie.

**Mesure** : temps de traitement d'un cycle de paie, avant et après. C'est le premier point
où la promesse d'accélération devient vérifiable.

## Phase 4 — Chantier et fournisseurs (8 à 10 semaines)

- Codes de coût, imputation de la main-d'œuvre au coût chargé réel.
- Comptes fournisseurs avec extraction et ventilation assistées.
- Budget vs réel, projection à l'achèvement.
- Facturation progressive avec retenues contractuelles.

## Phase 5 — Comptabilité et pilotage

- Grand livre complet ou consolidation de l'export vers le système existant.
- TPS/TVQ, conciliation bancaire assistée.
- Tableaux de bord, interrogation en langage naturel.

## Jalons de décision

| Jalon | Question | Si la réponse est non |
|---|---|---|
| Fin phase 0 | La CCQ accepte-t-elle nos fichiers ? | Arrêt, ou intégration à un logiciel existant plutôt que remplacement |
| Fin phase 1 | Écart de 0,00 $ sur 12 mois ? | On corrige jusqu'à l'obtenir. Aucune dérogation. |
| Fin phase 2 | Trois cycles en parallèle sans écart ? | On prolonge le parallèle |
| Fin phase 3 | Le temps administratif a-t-il baissé de façon mesurable ? | On revoit l'usage de l'IA, on ne l'étend pas |

## Charge récurrente à budgéter dès le départ

La veille et la mise à jour du référentiel de conventions ne s'arrêtent jamais. Un projet
qui n'a pas prévu qui fait ce travail, et avec quel budget annuel, échouera à la première
révision de convention — pas au développement.
