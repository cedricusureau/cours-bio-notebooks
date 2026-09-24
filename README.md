# Notebook 1 — De l'ADN du patient à la protéine

Support de la journée de remise à niveau biologie (public info / data, débutants Python).
Fil rouge : la drépanocytose — une seule lettre change dans le gène *HBB*.

Le notebook part de quatre gènes de globine exprimés dans le globule rouge — `HBA1`, `HBB`,
`HBD`, `HBG1` — séquencés chez un sujet de référence et chez le patient. La première question
est de trouver **lequel des quatre est muté** ; la suite en déroule l'effet, du nucléotide
jusqu'à l'acide aminé.

Les séquences sont les séquences codantes RefSeq réelles (`NM_000518.5`, `NM_000558.5`,
`NM_000519.4`, `NM_000559.3`). Seul `HBB` diffère chez le patient, d'une base.

## Ouvrir le notebook

Page d'accueil, à donner aux participants :
**https://cedricusureau.github.io/cours-bio-notebooks/**

Ou directement, selon le niveau :

| Niveau | Ce qui est fourni | Lien |
|---|---|---|
| 🟢 Facile | Le code est écrit, les `___` sont à compléter | [Colab](https://colab.research.google.com/github/cedricusureau/cours-bio-notebooks/blob/main/notebook1_facile.ipynb) |
| 🟡 Moyen | Les étapes sont en commentaire, le code est à écrire | [Colab](https://colab.research.google.com/github/cedricusureau/cours-bio-notebooks/blob/main/notebook1_moyen.ipynb) |
| 🔴 Difficile | Seule la consigne est donnée | [Colab](https://colab.research.google.com/github/cedricusureau/cours-bio-notebooks/blob/main/notebook1_difficile.ipynb) |

Les trois versions posent les mêmes questions et aboutissent au même résultat. On peut changer de
niveau en cours de route.

## Ce dont le notebook a besoin

Rien d'autre qu'un compte Google. Les séquences FASTA sont écrites en dur dans la première cellule,
qui les écrit sur le disque de la session puis les relit — aucune bibliothèque externe n'est
installée, aucun fichier n'est téléchargé. `data/` contient les deux mêmes fichiers multi-FASTA
(`reference.fasta`, `patient.fasta`), pour référence.

## Corrigé

`notebook1_corrige.ipynb` n'est pas publié tant que la séance n'a pas eu lieu : il est exclu par le
`.gitignore`. Pour le mettre en ligne, retirer sa ligne du `.gitignore` puis committer.
