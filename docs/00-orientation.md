# 0. Orientation — le vrai problème à régler

> **Ce document prime sur les cinq suivants.** Les documents 01 à 05 décrivent le
> remplacement d'Avantage. Ce n'est **pas** ce qu'il faut faire maintenant.

## 0.1 Reformulation

Le besoin réel n'est pas « remplacer Avantage ». C'est : **le cycle de paie prend trop de
temps dans une entreprise qui utilise déjà Avantage et qui en est satisfaite sur le fond.**

Remplacer Avantage pour régler ça, c'est prendre 6 à 12 mois de développement et tout le
risque réglementaire de la conformité CCQ… pour corriger un problème qui est, dans la
quasi-totalité des cas, un problème de **saisie**, pas de calcul.

Avantage calcule vite. C'est **l'alimentation** d'Avantage qui est lente.

## 0.2 Recommandation : la passerelle, pas le remplacement

```
   Chantier                    Nouvel outil                    Avantage
 ┌───────────┐            ┌──────────────────────┐         ┌──────────────┐
 │ Contremaître│  saisie  │ Saisie mobile        │ fichier │ Paie         │
 │ téléphone   ├─────────►│ Photo → extraction IA├────────►│ Conventions  │
 │ ou papier   │          │ Contrôles d'anomalies│ d'import│ Retenues     │
 └───────────┘            │ Validation admin     │         │ Rapport CCQ  │
                          └──────────────────────┘         │ T4 / RL-1    │
                                    ▲                      └──────┬───────┘
                                    └─── employés, chantiers ─────┘
                                         (synchronisation en lecture)
```

Avantage reste le système de référence. Il garde la paie, les taux de convention, les
retenues à la source, le rapport mensuel CCQ, les T4 et les Relevés 1. Le nouvel outil ne
transporte **que des heures**.

### Pourquoi c'est le bon choix

| | Passerelle | Remplacement |
|---|---|---|
| Délai avant premier gain | 4 à 8 semaines | 12 à 18 mois |
| Risque réglementaire | **Nul** — on ne calcule rien | Élevé et permanent |
| Veille des conventions collectives | Aucune, Avantage la fait | 0,3 à 0,5 ETP, indéfiniment |
| Responsabilité en cas d'erreur de paie | Reste chez l'éditeur | Passe chez nous |
| Réversibilité | Totale : on revient au papier | Aucune, une fois basculé |
| Part du gain de temps capté | 70 à 85 % | 100 % |

La passerelle capte l'essentiel du gain pour une fraction du coût et du risque. Et elle
construit au passage un historique de temps propre et structuré — exactement ce qu'il
faudrait si un remplacement devenait un jour souhaitable.

## 0.3 Le point à vérifier en premier

**Avantage accepte-t-il un fichier d'import de feuilles de temps ?**

Appel à l'éditeur, ou vérification dans le contrat de soutien. Trois cas :

1. **Import documenté** (CSV, fichier texte, interface) → cas idéal, on développe contre ce format.
2. **Accès en lecture/écriture à la base de données** → faisable, avec prudence : écriture
   uniquement dans les tables de saisie de temps, jamais dans les tables de calcul.
3. **Ni l'un ni l'autre** → automatisation de la saisie à l'écran. Moins propre, plus
   fragile aux mises à jour, mais le gain reste réel. À évaluer seulement dans ce cas.

Une lecture seule de la base (liste des salariés, des chantiers, des codes d'activité) est
utile dans tous les cas et sans risque.

## 0.4 Le produit minimal — 4 à 8 semaines

1. **Synchronisation** des salariés, chantiers et codes d'activité depuis Avantage, en
   lecture seule.
2. **Saisie par le contremaître sur téléphone** : choisir le chantier, cocher son équipe,
   entrer les heures et les primes. Fonctionne **hors ligne** et se synchronise plus tard —
   le réseau en chantier n'est pas fiable.
3. **Pré-remplissage** à partir de la semaine précédente. Une équipe change peu d'une
   semaine à l'autre : c'est ce qui fait passer une saisie de vingt minutes à deux minutes.
4. **Photo de feuille papier → extraction assistée par IA**, pour ceux qui ne passeront pas
   au téléphone. L'extraction est proposée, l'humain corrige.
5. **Écran de validation unique** pour l'administration, avec les anomalies en tête de
   liste plutôt que noyées.
6. **Génération du fichier d'import** pour Avantage, après approbation explicite.

## 0.5 Où l'IA sert dans ce périmètre

- **Extraction des feuilles papier** : photo → salarié, chantier, jour, heures, primes.
- **Détection d'anomalies avant l'envoi** : heures invraisemblables, salarié déclaré sur
  deux chantiers au même moment, métier inhabituel pour ce salarié, chantier clos, écart
  marqué avec les semaines précédentes.
- **Apprentissage des habitudes** : quelle équipe sur quel chantier, quels codes d'activité
  reviennent — pour proposer, jamais pour décider.

Et rien d'autre. **L'outil ne calcule aucun montant.** Il produit des heures validées par
un humain. Tout le reste appartient à Avantage.

## 0.6 Informations nécessaires pour chiffrer

- Nombre de salariés, de contremaîtres, de chantiers actifs simultanément.
- Comment les heures arrivent aujourd'hui : papier, texto, appel téléphonique, Excel ?
- Combien d'heures par semaine sur la paie, et réparties comment entre la collecte, la
  ressaisie, les corrections et le rapport mensuel ?
- L'irritant principal : la collecte, la ressaisie, ou les corrections du rapport CCQ ?
- Version d'Avantage et état du contrat de soutien.

Si l'irritant principal se révèle être ailleurs — le rapport mensuel CCQ, ou l'imputation
aux chantiers — la passerelle change de forme, mais le principe tient : **un outil autour
d'Avantage, pas à sa place.**

## 0.7 Et le remplacement ?

Les documents 01 à 05 restent valables comme étude, et comme réponse à la question
« est-ce possible ? ». La réponse était oui. Mais on ne s'engage pas là-dedans pour régler
un problème de saisie de feuilles de temps. Cette piste se rouvre seulement si Avantage
devient bloquant sur le fond — coût, fin de support, fonction manquante irremplaçable — et
pas avant.
