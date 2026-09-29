# labo-book — Cahier de laboratoire (3275.1)

Cahier de laboratoire du cours **3275.1 — Conception d'opérations de sécurité**,
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
| Annotations inline | Hypothesis (groupe privé) — surlignage + commentaire dans la marge |
| Commentaires par page | giscus (GitHub Discussions) — bas de page |

## Structure du dépôt

```
labo-book/
├── _quarto.yml                  # config du site (navigation + commentaires)
├── styles.scss                  # thème « ingénieur » (palette, typographie)
├── includes/fonts.html          # Inter + JetBrains Mono
├── index.qmd                    # page d'accueil
├── relecture.qmd                # guide de relecture destiné au prof
├── labos/
│   ├── chapitre-01/
│   │   ├── activite-1-1.qmd     # modèle complet
│   │   └── activite-1-2.qmd     # modèle court
│   └── chapitre-02/
│       └── activite-2-1.qmd
├── .github/workflows/publish.yml  # CI : render + deploy
└── README.md
```

## Workflow quotidien

```bash
quarto preview                 # aperçu local en temps réel
# ... éditer / créer un .qmd ...
git add .
git commit -m "labo-1-2: ..."
git push                       # → site régénéré en ~1-2 min
```

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

### 2. giscus (commentaires en bas de page)

1. **Settings → Discussions** : activer les Discussions du dépôt.
2. Ouvrir <https://giscus.app>, renseigner le dépôt `Marc-Pillonel/labo-book`,
   choisir la catégorie (généralement **General**).
3. Copier `repo-id` / `category-id` dans `_quarto.yml`
   (`repo-id` est déjà renseigné ; `category-id` est à compléter).
4. Installer l'app **giscus** sur le dépôt (bouton « Enable » proposé par giscus).

### 3. Hypothesis (annotations dans le texte)

1. Créer un compte gratuit : <https://hypothes.is/signup>.
2. Créer un **groupe privé** (ex. « Labo 3275 ») depuis la sidebar Hypothesis.
3. Envoyer le lien d'invitation au prof **par email** (ne pas le publier :
   ce lien donne accès au groupe).
4. L'activer sur le site est déjà fait (`website.comments.hypothesis` dans
   `_quarto.yml`).

> ⚠️ Les annotations sont **publiques par défaut** : le prof doit sélectionner
> le groupe dans la sidebar (une fois pour toutes, la sélection est mémorisée).

## Notes d'exploitation

- **Visibilité** : dépôt et site sont publics — tout le monde peut *lire* le
  cahier. Les annotations Hypothesis du groupe privé restent confidentielles ;
  les commentaires giscus sont publics (Discussions GitHub ouvertes).
- **Notifications** : emails Hypothesis pour les réponses/mentions ; pour les
  nouvelles annotations, consulter la sidebar de temps en temps.
- **OneDrive** : ce dépôt vit dans un dossier synchronisé par OneDrive. En cas
  de conflits (`fichier (conflict).md`, `.git` verrouillé), déplacer le dépôt
  hors d'OneDrive ou exclure le dossier de la synchronisation.
