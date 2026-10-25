# labo-book - Cahier de laboratoire (3275.1)

Cahier de laboratoire du cours **3275.1 - Conception d'opérations de sécurité**,
rédigé en Markdown (Quarto), publié automatiquement sur GitHub Pages, avec
relecture annotée en ligne.

- **Site en ligne** : <https://marc-pillonel.github.io/labo-book/>
- **Dépôt** : <https://github.com/Marc-Pillonel/labo-book>

## Architecture

| Couche | Outil |
|---|---|
| Rédaction locale | Quarto (`.qmd` = Markdown + YAML), preview live |
| Versionnement | Git / GitHub |
| Déploiement | GitHub Action → GitHub Pages (à chaque *push* sur `main`) |
| Annotations inline | Hypothesis (groupe privé `labo-book`) - surlignage + commentaire dans la marge |

## Structure du dépôt

```
labo-book/
├── _quarto.yml                  # config du site (navigation + annotations)
├── styles.scss                  # thème « ingénieur » (palette, typographie)
├── includes/fonts.html          # Inter + JetBrains Mono
├── index.qmd                    # page d'accueil
├── relecture.qmd                # guide de relecture destiné au prof
├── rapport-activite-template.xls  # rapport d'activité (heures, mis à jour chaque semaine)
├── labos/
│   ├── chapitre-01/             # activités 1 à 9 (introduction)
│   ├── chapitre-02/             # activités 10 et 11 (conception en entreprise)
│   ├── chapitre-03/             # activité 12 (MCSR) + src/ (diagrammes)
│   └── intervention/            # compte rendu d'intervention
├── .github/workflows/publish.yml  # CI : render + deploy
└── README.md
```

Les supports du cours (méthode MCSR, slides, fiche du mini-cas) restent
localement dans `labos/chapitre-03/03_MCSR/` et `Partage activité MCSR.pdf` :
ils sont exclus par `.gitignore` pour ne pas être republiés sur le site.

## Workflow quotidien

```bash
quarto preview                 # aperçu local en temps réel
# ... éditer / créer un .qmd ...
git add .
git commit -m "labo-1-2: ..."
git push                       # → site régénéré en ~1-2 min
```

Chaque semaine : mettre à jour `rapport-activite-template.xls` (heures
réalisées) et vérifier la structuration du cahier, conformément au
`devoirs.md` du cours.

### Ajouter une activité

1. Créer `labos/chapitre-XX/activite-X-Y.qmd` (se baser sur `activite-1-1.qmd`).
2. La sidebar l'affiche automatiquement (dossier référencé dans `_quarto.yml`).
3. Nommer les fichiers avec un numéro pour conserver l'ordre (alphabetique).

### Ajouter un chapitre

1. Créer le dossier `labos/chapitre-XX/`.
2. Ajouter dans `_quarto.yml`, sous `website.sidebar.contents` :

```yaml
- section: "Chapitre 3"
  contents: labos/chapitre-03/*
```

## Configuration manuelle (à faire sur GitHub / Hypothesis)

> Ces étapes nécessitent l'interface web et ne peuvent pas être automatisées.

### 1. GitHub Pages (activation une seule fois, manuelle)

GitHub impose ce clic une fois par dépôt (l'API interdit l'activation via le
`GITHUB_TOKEN` des workflows) :

1. **Settings → Pages → Build and deployment → Source** : **GitHub Actions**.
2. Relancer le dernier run (onglet **Actions → ⋯ → Re-run all jobs**) ou
   pousser une modification : le site est déployé à chaque *push* sur `main`.

### 2. Hypothesis (annotations dans le texte) - fait le 2026-09-29

1. Compte gratuit créé, **groupe privé** `labo-book` créé :
   <https://hypothes.is/groups/yR9P8X3a/labo-book>
2. Annotation intégrées au site via `website.comments.hypothesis` (`_quarto.yml`).
3. Reste à faire : **inviter le prof** sur le groupe et lui signaler qu'il doit
   **sélectionner le groupe** dans la sidebar (par défaut « Public » - sinon
   ses annotations restent publiques et hors du groupe).

> ⚠️ Le lien du groupe est public sur ce dépôt : quiconque le suit peut
> rejoindre le groupe et lire les annotations. Régénérer un groupe si cela
> devient un souci.

## Notes d'exploitation

- **Visibilité** : dépôt et site sont publics - tout le monde peut *lire* le
  cahier. Les annotations postées dans le groupe privé `labo-book` ne sont
  visibles que par ses membres (relecteur + auteur).
- **Notifications** : emails Hypothesis pour les réponses/mentions ; pour les
  nouvelles annotations, consulter la sidebar de temps en temps.
- **OneDrive** : ce dépôt vit dans un dossier synchronisé par OneDrive. En cas
  de conflits (`fichier (conflict).md`, `.git` verrouillé), déplacer le dépôt
  hors d'OneDrive ou exclure le dossier de la synchronisation.
