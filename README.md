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

## Notebook 2 — De l'ADN du patient à l'hémoglobine en 3D

Le notebook commence par l'ADN du patient : quatre gènes de globine exprimés dans le globule
rouge — `HBA1`, `HBB`, `HBD`, `HBG1` — séquencés chez un sujet de référence et chez le patient.
Il faut trouver **lequel des quatre est muté**, puis la base, le codon et l'acide aminé modifiés
(sections 1 à 3). Les séquences sont les séquences codantes RefSeq réelles (`NM_000518.5`,
`NM_000558.5`, `NM_000519.4`, `NM_000559.3`) ; seul `HBB` diffère chez le patient, d'une base.
`data/` contient les deux fichiers multi-FASTA (`reference.fasta`, `patient.fasta`).

Le notebook passe ensuite de la séquence à la structure : la chaîne β du patient a-t-elle la même forme
que la chaîne normale, et sinon, qu'est-ce que la valine 6 change ? Il compare deux sources : les
prédictions d'AlphaFold 3 que les participants lancent sur le serveur AlphaFold (tétramère de
2 chaînes α, 2 chaînes β et 4 hèmes, en version normale et en version patient), et les structures
expérimentales `2HHB` (hémoglobine normale) et `2HBS` (hémoglobine S). Cinq fonctions à écrire, en
Python pur : pLDDT moyen, distance entre deux atomes, écart de repliement (dRMSD), nombre de
voisins d'un résidu, distance minimale entre deux résidus. Durée visée : 45 à 60 minutes au
niveau 🟡 pour cette partie structure, plus le temps des sections 1 à 3 (non mesuré).

| Niveau | Lien |
|---|---|
| 🟢 Facile | [Colab](https://colab.research.google.com/github/cedricusureau/cours-bio-notebooks/blob/main/notebook2_facile.ipynb) |
| 🟡 Moyen | [Colab](https://colab.research.google.com/github/cedricusureau/cours-bio-notebooks/blob/main/notebook2_moyen.ipynb) |
| 🔴 Difficile | [Colab](https://colab.research.google.com/github/cedricusureau/cours-bio-notebooks/blob/main/notebook2_difficile.ipynb) |

**Ce dont il a besoin.** Un compte Google, pour Colab et pour le serveur AlphaFold
(alphafoldserver.com), et le réseau. La première cellule installe `py3Dmol`
(`!pip install py3Dmol`), seule bibliothèque externe. Les structures sont téléchargées depuis la
PDB (RCSB) et AlphaFold DB, avec repli sur la copie de `data/`. Quand un participant n'a pas déposé
ses prédictions, le notebook prend les prédictions de secours de `data/`, et à défaut le modèle
AlphaFold DB de la chaîne β seule.

Fichiers de `data/` utilisés par ce notebook :

| Fichier | Contenu | Source |
|---|---|---|
| `2HHB.pdb` | désoxyhémoglobine humaine normale (rayons X, 1,74 Å) | RCSB PDB |
| `2HBS.pdb` | désoxyhémoglobine S, deux tétramères (rayons X, 2,05 Å) | RCSB PDB |
| `AF-P68871-F1-model_v6.pdb` | chaîne β seule (UniProt P68871, méthionine comprise), pLDDT dans le champ B | AlphaFold DB, licence CC-BY 4.0 |
| `af3_hb_normal.json`, `af3_hb_patient.json` | les deux jobs du serveur AlphaFold (dialecte `alphafoldserver`, version 1) | générateur du notebook |
| `af3_hb_normal.cif`, `af3_hb_patient.cif` | prédictions de secours — **à déposer** | serveur AlphaFold |

Pour produire les prédictions de secours (une fois, avec le compte du formateur) : sur
alphafoldserver.com, importer les deux JSON (*Upload JSON*), lancer les deux jobs, télécharger les
deux `.zip`, puis copier le fichier `…_model_0.cif` de chacun dans `data/`, sous les noms
`af3_hb_normal.cif` et `af3_hb_patient.cif`.

Les quatre notebooks et les fichiers de `data/`, sauf les `.cif`, sont produits par
`tools/gen_notebook2.py`, dans le projet du cours (hors de ce dépôt) : ne pas éditer les `.ipynb` à
la main.

## Corrigés

`notebook1_corrige.ipynb` et `notebook2_corrige.ipynb` ne sont pas publiés tant que la séance n'a
pas eu lieu : ils sont exclus par le `.gitignore`. Pour publier l'un d'eux, retirer sa ligne du
`.gitignore` puis committer.
