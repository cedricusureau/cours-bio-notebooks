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
| `af3_hb_normal.json`, `af3_hb_patient.json` | les deux demandes au serveur AlphaFold, à importer avec *Upload JSON*. Réservées au formateur, pour qui bloque sur le copier-coller : elles contiennent les séquences que le notebook fait reconstruire. La page d'accueil n'y renvoie pas ; elles se téléchargent depuis `corriges.html` (onglet Notebook 2) |
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

## Notebook 3 (bonus) — Pourquoi cette mutation ?

Les homozygotes SS ont la drépanocytose, et pourtant l'allèle HbS dépasse 15 % dans plusieurs pays
d'Afrique. Pourquoi ? Le notebook ne donne pas la réponse : elle se déduit des données, en deux
parties.

1. **Où trouve-t-on l'allèle HbS, et pourquoi là ?** Le tableau par pays : les pays classés par
   fréquence de l'allèle, puis par nombre de naissances SS ; moyennes par région OMS. Ensuite,
   trois maladies infectieuses candidates (tuberculose, VIH, paludisme) : trois nuages de points,
   et le coefficient de corrélation de Pearson écrit à la main, sur tous les pays puis sur la
   seule région Afrique. Une étude cas-témoins suit : le pourcentage d'enfants AS dans quatre
   groupes de malades en Gambie (Hill et al. 1991), et les rapports des cotes. Enfin, les pays qui
   s'écartent de la tendance.
2. **Une mutation neuve : se perd-elle ou s'installe-t-elle ?** Modèle de Wright-Fisher avec
   sélection, en Python pur (`random`) : une génération, une trajectoire, puis 1 000 trajectoires,
   avec et sans l'avantage des hétérozygotes AS. Environ 3 mutations neuves sur 4 sont perdues par
   dérive malgré cet avantage, le même ordre de grandeur que les simulations de Shriner et Rotimi
   (2018) : 74,6 %.

| Niveau | Lien |
|---|---|
| 🟢 Facile | [Colab](https://colab.research.google.com/github/cedricusureau/cours-bio-notebooks/blob/main/notebook3_facile.ipynb) |
| 🟡 Moyen | [Colab](https://colab.research.google.com/github/cedricusureau/cours-bio-notebooks/blob/main/notebook3_moyen.ipynb) |
| 🔴 Difficile | [Colab](https://colab.research.google.com/github/cedricusureau/cours-bio-notebooks/blob/main/notebook3_difficile.ipynb) |

**Ce dont il a besoin.** Un compte Google. Le tableau est écrit en dur dans la première cellule ;
les graphiques utilisent `matplotlib`, déjà installé dans Colab. Rien n'est téléchargé. Le
corrigé s'exécute en quelques secondes.

`data/hbs_par_pays.csv` contient une ligne par pays ou territoire : 190 lignes, soit la table
source entière moins le Sahara occidental, qui n'a de région OMS dans aucune des deux sources.

| Colonne | Contenu | Source |
|---|---|---|
| `pays`, `code_iso3` | nom français, code ISO 3166-1 alpha-3 | ISO 3166-1 (`pycountry`) |
| `region_oms` | région OMS | OMS, Global Health Observatory (à défaut : Piel 2013) |
| `frequence_allele_hbs` | fréquence de l'allèle HbS estimée pour 2010, médiane | Piel et al. 2013, appendix, Web Table 1 |
| `nombre_enquetes` | nombre d'enquêtes utilisées par le modèle pour ce pays | idem |
| `naissances_ss_par_an` | nouveau-nés SS par an en 2010, médiane | idem |
| `incidence_paludisme_2000` | cas de paludisme estimés pour 1 000 habitants exposés, en 2000 ; vide sans estimation OMS | OMS, Global Health Observatory, `MALARIA_EST_INCIDENCE` |
| `incidence_tuberculose_2000` | cas de tuberculose pour 100 000 habitants, en 2000 ; vide sans donnée | OMS, Global Health Observatory, `MDG_0000000020` |
| `prevalence_vih_2000` | % des adultes de 15 à 49 ans vivant avec le VIH, en 2000 ; l'OMS publie « <0.1 » avec 0,1 comme valeur numérique, reprise telle quelle ; vide sans donnée | OMS, Global Health Observatory, `MDG_0000000029` |

Le fichier est produit par `tools/data_notebook3.py`, dans le projet du cours. Ce script extrait
la Web Table 1 du PDF de l'annexe et interroge l'API de l'OMS. Les quatre notebooks sont produits
par `tools/gen_notebook3.py` : ne pas éditer les `.ipynb` à la main.

**Sources et conditions de réutilisation.**
- Piel FB et al. *Lancet* 2013;381:142–151, doi:10.1016/S0140-6736(12)61229-X. Le tableau
  reprend des valeurs numériques de la Web Table 1, avec cette référence. Le PDF de l'annexe
  (© Elsevier) n'est pas redistribué.
- OMS, Global Health Observatory, indicateurs `MALARIA_EST_INCIDENCE` (*Estimated malaria
  incidence per 1000 population at risk*), `MDG_0000000020` (*Incidence of tuberculosis per
  100 000 population per year*) et `MDG_0000000029` (*Prevalence of HIV among adults aged 15 to
  49, %*), année 2000, consultés en septembre 2026. Réutilisation selon
  les [conditions de l'OMS pour ses données](https://www.who.int/about/policies/publishing/data-policy/terms-and-conditions).
- Chiffres cités dans le texte : Piel et al. 2010 (*Nat Commun* 1:104), Hay et al. 2004 (*Lancet
  Infect Dis* 4:327), Taylor et al. 2012 (*Lancet Infect Dis* 12:457 ; son tableau des études
  cas-témoins fournit les effectifs de Hill et al. 1991, *Nature* 352:595), Grosse et al. 2011 (*Am J
  Prev Med* 41:S398), Shriner et Rotimi 2018 (*Am J Hum Genet* 102:547), Ojodu et al. 2014
  (*MMWR* 63:1155), Flint et al. 1986 (*Nature* 321:744). Les effectifs d'Ibadan (AA 9 365,
  AS 2 993, SS 29) sont cités d'après F. J. Ayala, *Encyclopædia Britannica*, article
  « Evolution ». Leur publication d'origine n'a pas été retrouvée.

## Corrigés

`notebook1_corrige.ipynb`, `notebook2_corrige.ipynb` et `notebook3_corrige.ipynb` ne sont pas
publiés tant que la séance n'a pas eu lieu : ils sont exclus par le `.gitignore`. Pour publier
l'un d'eux, retirer sa ligne du `.gitignore` puis committer.

**Version chiffrée, pour le formateur :
[corriges.html](https://cedricusureau.github.io/cours-bio-notebooks/corriges.html).** La page
contient les trois corrigés déjà exécutés, avec leurs sorties et leurs figures. Un bouton permet
aussi de télécharger le `.ipynb` exécuté, à ouvrir dans Colab (*Fichier → Importer un notebook*).
Elle ne s'ouvre qu'avec le mot de passe : sans lui, elle ne contient que du texte chiffré
(AES-256-GCM, clé dérivée du mot de passe par PBKDF2-SHA256, 600 000 itérations). Le
déchiffrement se fait dans le navigateur.

La page est produite par `tools/gen_corriges.py`, dans le projet du cours, qui exécute les
corrigés puis chiffre le résultat. Le mot de passe n'est pas dans ce dépôt. Relancer le script
après chaque modification d'un notebook.
