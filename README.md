# Accélérer le cycle de paie d'un entrepreneur en construction (Québec)

L'entreprise utilise **Avantage** et en est satisfaite. Le problème est le **temps** que
prend le cycle de paie — pas le logiciel de paie lui-même.

**Orientation retenue : construire une passerelle en amont d'Avantage, pas un remplacement.**
Saisie de temps mobile en chantier, extraction assistée par IA des feuilles papier,
contrôles d'anomalies, puis fichier d'import vers Avantage. Avantage garde la paie, les
conventions collectives, les retenues, le rapport mensuel CCQ et les fins d'année.

👉 **Commencer par [docs/00-orientation.md](docs/00-orientation.md).**

## Documents

| Document | Contenu | Statut |
|---|---|---|
| [00-orientation](docs/00-orientation.md) | **Le vrai problème, la solution recommandée, le produit minimal** | ✅ Actif |
| [01-faisabilite](docs/01-faisabilite.md) | Faisabilité d'un remplacement d'Avantage : verdict et obstacles | 📚 Étude |
| [02-perimetre](docs/02-perimetre.md) | Périmètre fonctionnel complet d'un tel logiciel | 📚 Étude |
| [03-architecture](docs/03-architecture.md) | Architecture d'un système de paie construction | 📚 Étude |
| [04-ia](docs/04-ia.md) | Usages de l'IA et garde-fous — **s'applique aussi à la passerelle** | ✅ Actif |
| [05-plan](docs/05-plan.md) | Plan de livraison d'un remplacement complet | 📚 Étude |

Les documents marqués « Étude » répondent à la question « est-ce possible ? ». La réponse
est oui, mais ce n'est pas la voie retenue pour le besoin actuel.

## Prochaine étape

Une seule question bloquante : **Avantage accepte-t-il un fichier d'import de feuilles de
temps, et sous quel format ?** À poser à l'éditeur. Tout le reste en découle.

## Avertissement

Les informations réglementaires citées dans ces documents (CCQ, conventions collectives,
retenues à la source) proviennent d'une connaissance générale du domaine. Elles doivent
être validées auprès des sources officielles avant toute implémentation.
