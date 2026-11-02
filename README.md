# Point de Marché — agent IA de briefings de marché (Financial Times)

> Trois briefings de marché par jour, rédigés en français à partir du *Financial Times*, avec une
> lecture par corrélations plutôt qu'une simple revue de presse.

🌐 **Site du projet :** [anatole-point-de-marche.netlify.app](https://anatole-point-de-marche.netlify.app)

---

## Le problème

Lire la presse financière prend du temps, et le plus dur n'est pas de savoir *ce qui s'est passé* :
c'est de comprendre **pourquoi les variables bougent ensemble**. Le dollar monte, l'or recule, les
taux longs se tendent — ces mouvements ne sont presque jamais indépendants, mais aucun flux
d'actualités ne reconstruit l'enchaînement de causalité pour vous.

J'ai donc construit un agent IA qui le fait, trois fois par jour.

## Ce que fait l'agent

| | Briefing | Contenu |
|---|---|---|
| ☀️ | **Matin** | Ce qui s'est passé pendant la nuit (Asie), agenda du jour, ce qu'il faut surveiller |
| 🌤️ | **Midi** | Ouverture européenne, réaction aux publications de la matinée |
| 🌙 | **Soir** | Clôture Europe, ouverture Wall Street, synthèse de la journée |

Chaque briefing est produit sous forme de **PDF**, en français.

## Comment ça marche

```
Financial Times (navigation en direct)
        │
        ▼
  Lecture et sélection des articles      ──  tri par géographie et par thème
        │
        ▼
  Analyse des corrélations               ──  sens du lien, score de force 1–5, raisonnement
        │
        ▼
  Synthèse et hiérarchisation            ──  ce qui compte vraiment aujourd'hui
        │
        ▼
  Génération du PDF
```

**Pile technique :** Claude (modèle de langage) + Claude in Chrome pour la navigation en direct sur
le Financial Times + génération de PDF. L'agent lit les articles sur le site au moment où il
travaille : les briefings portent donc sur l'actualité réelle du jour, et non sur des connaissances
figées dans le modèle.

## Structure d'un briefing

1. **Articles classés par géographie et par thème** — États-Unis, Europe, Asie, matières premières,
   crédit, crypto…
2. **Analyse de corrélations** — pour chaque lien identifié entre deux variables : le sens du lien,
   un score de force de 1 à 5, et le raisonnement qui le justifie.
3. **Tableau récapitulatif** — les mouvements de la séance en un coup d'œil.
4. **« Si tu n'en lis que trois »** — les trois idées à retenir si on ne lit rien d'autre.
5. **À surveiller** — les publications, réunions et échéances à venir.

### Exemple d'analyse de corrélation

| Variable A | Variable B | Sens | Force | Raisonnement |
|---|---|---|:---:|---|
| Taux réels américains | Or | Inverse | 4/5 | Des taux réels plus élevés augmentent le coût d'opportunité de détenir un actif qui ne verse aucun rendement. |
| Dollar | Actions émergentes | Inverse | 4/5 | Un dollar fort renchérit la dette libellée en dollars et resserre les conditions de financement des émergents. |
| Pétrole | Point mort d'inflation | Positif | 3/5 | L'énergie se transmet rapidement aux anticipations d'inflation, puis aux attentes de politique monétaire. |

> Les chiffres ci-dessus illustrent le format, pas un briefing en particulier.

## Pourquoi ce projet

Je m'intéresse aux marchés financiers et je veux comprendre leurs mécanismes, pas seulement en
suivre l'actualité. Ce projet est l'outil que j'utilise pour ça au quotidien, et il m'a aussi servi
à apprendre à concevoir un agent IA de bout en bout : définition de la tâche, accès aux sources,
format de sortie, contrôle de la qualité.

Les briefings publiés ne contiennent aucune information sur un portefeuille ou des positions :
l'objet du projet est l'analyse, pas le conseil en investissement.

## Projets liés

- 🌐 [Site vitrine du projet](https://anatole-point-de-marche.netlify.app) — présentation de l'agent
- 📊 **Météo des Marchés** — baromètre public Risk-On / Risk-Off (score 0–100 sur 8 indicateurs cross-asset)

## Contact

- **LinkedIn :** [anatole-hours-wohleber](https://www.linkedin.com/in/anatole-hours-wohleber)
- **E-mail :** anatolewohleberhours@gmail.com

---

<sub>Projet personnel d'apprentissage. Le contenu des briefings est produit pour un usage privé à
partir d'un abonnement personnel au Financial Times ; aucun article n'est reproduit ni redistribué
ici. Rien dans ce dépôt ne constitue un conseil en investissement.</sub>
