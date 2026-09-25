# Notebooks — remise à niveau biologie

Support de la journée de remise à niveau biologie (public info / data, débutants Python).
Fil rouge : la drépanocytose — une seule lettre change dans le gène *HBB*.

Page d'accueil, à donner aux participants :
**https://cedricusureau.github.io/cours-bio-notebooks/**

Chaque notebook existe en trois versions, qui posent les mêmes questions et aboutissent au même
résultat ; seule la quantité de code fourni change. On peut changer de niveau en cours de route.

| Niveau | Ce qui est fourni |
|---|---|
| 🟢 Facile | Le code est écrit, les `___` sont à compléter |
| 🟡 Moyen | Les étapes sont en commentaire, le code est à écrire |
| 🔴 Difficile | Seule la consigne est donnée |

## Notebook 1 — De l'ADN à la protéine

Le notebook part de la séquence codante du gène *HBB* (RefSeq `NM_000518.5`), chez un sujet de
référence, et suit le dogme central : transcription, découpage en codons, traduction, jusqu'à la
bêta-globine (147 acides aminés, méthionine initiale comprise). Pas de patient ni de mutation :
ils arrivent au notebook 2.

| Niveau | Lien |
|---|---|
| 🟢 Facile | [Colab](https://colab.research.google.com/github/cedricusureau/cours-bio-notebooks/blob/main/notebook1_facile.ipynb) |
| 🟡 Moyen | [Colab](https://colab.research.google.com/github/cedricusureau/cours-bio-notebooks/blob/main/notebook1_moyen.ipynb) |
| 🔴 Difficile | [Colab](https://colab.research.google.com/github/cedricusureau/cours-bio-notebooks/blob/main/notebook1_difficile.ipynb) |

**Ce dont il a besoin.** Rien d'autre qu'un compte Google. La séquence FASTA est écrite en dur
dans la première cellule, qui l'écrit sur le disque de la session puis la relit — aucune
bibliothèque externe n'est installée, aucun fichier n'est téléchargé. Elle est tirée de
`data/reference.fasta`.

## Notebook 2 — Du patient à AlphaFold

Le notebook part de l'ADN du patient : quatre gènes de globine exprimés dans le globule rouge —
`HBA1`, `HBB`, `HBD`, `HBG1` — séquencés chez un sujet de référence et chez le patient. Les
séquences sont les séquences codantes RefSeq réelles (`NM_000518.5`, `NM_000558.5`,
`NM_000519.4`, `NM_000559.3`) ; seul `HBB` diffère chez le patient, d'une base.

1. quel gène est muté, quelle base, quel codon, quel acide aminé ;
2. ce changement d'acide aminé est-il important (classe de la chaîne latérale : chargé,
   polaire, apolaire) ;
3. les séquences des chaînes matures, à coller dans le serveur AlphaFold (hémoglobine normale et
   hémoglobine du patient : 2 chaînes α, 2 chaînes β, 4 hèmes) ;
4. regarder le résultat sur le serveur, puis dans une vue 3D fournie qui superpose les deux
   prédictions du cours.

| Niveau | Lien |
|---|---|
| 🟢 Facile | [Colab](https://colab.research.google.com/github/cedricusureau/cours-bio-notebooks/blob/main/notebook2_facile.ipynb) |
| 🟡 Moyen | [Colab](https://colab.research.google.com/github/cedricusureau/cours-bio-notebooks/blob/main/notebook2_moyen.ipynb) |
| 🔴 Difficile | [Colab](https://colab.research.google.com/github/cedricusureau/cours-bio-notebooks/blob/main/notebook2_difficile.ipynb) |

**Ce dont il a besoin.** Un compte Google, pour Colab et pour le serveur AlphaFold
(alphafoldserver.com), et le réseau pour la dernière cellule, qui installe `py3Dmol` et télécharge
les deux prédictions du cours depuis ce dépôt.

Fichiers de `data/` utilisés par ce notebook :

| Fichier | Contenu |
|---|---|
| `reference.fasta`, `patient.fasta` | les quatre gènes, référence et patient |
| `af3_hb_normal.json`, `af3_hb_patient.json` | les deux demandes au serveur AlphaFold, à importer avec *Upload JSON* (optionnel : on peut aussi coller les séquences) |
| `af3_hb_normal.cif`, `af3_hb_patient.cif` | prédictions d'AlphaFold 3 préparées pour le cours : meilleur modèle (`model_0`) de chaque job |

Les deux `.cif` sont des résultats d'AlphaFold Server, fournis sous les conditions
d'utilisation d'AlphaFold Server (« AlphaFold Server Output Terms of Use »,
[alphafoldserver.com/output-terms](https://alphafoldserver.com/output-terms)), dont le texte est
dans `data/AF3_OUTPUT_TERMS_OF_USE.md` : usage non commercial uniquement ; ce sont des modèles
théoriques, sans usage clinique.

`2HHB.pdb`, `2HBS.pdb` et `AF-P68871-F1-model_v6.pdb` servaient à une version précédente du
notebook (analyse 3D détaillée) ; le notebook actuel ne les utilise pas.

Les quatre notebooks sont produits par `tools/gen_notebook2.py`, dans le projet du cours (hors de
ce dépôt) : ne pas éditer les `.ipynb` à la main.

## Corrigés

`notebook1_corrige.ipynb` et `notebook2_corrige.ipynb` ne sont pas publiés tant que la séance n'a
pas eu lieu : ils sont exclus par le `.gitignore`. Pour publier l'un d'eux, retirer sa ligne du
`.gitignore` puis committer.
