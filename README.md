# Algorithme-de-Gillespie-Tumeurs
1. Par adaptation, les tumeurs développent des mécanismes pour éviter la réponse immunitaire. De
plus en plus, les traitements anti-cancéreux sont conçus pour solliciter les cellules immunitaires à
s’attaquer aux cellules tumorales pour encourager et augmenter l’élimination du cancer par les
mécanismes de la réponse immunitaire. Ceci peut inclure l’administration de cellules immunitaires
modifiées pour reconnaître la signature cancéreuse et cibler la tumeur ou des virus oncolytiques pour
augmenter la destruction de cellules tumorales. Oh et al. (2017) ont développé et testé un traitement
combiné impliquant la co-administration d’un virus oncolytique et de cellules dendritiques pour
améliorer et optimiser les effets anti-cancéreux de la thérapie. Sans traitement, la tumeur croît de
façon logistique selon l’équation
𝑑𝑆
𝑑𝑡
= 𝑟𝑆 &1 −
𝑆
𝐾
*
où 𝑆 représente les cellules tumorales (« susceptibles ») et 𝐾 la capacité de support de
l’environnement. Avec l’administration du traitement, les cellules immunitaires (surtout les
lymphocytes T) 𝑇 interagissent avec les cellules tumorales pour les éliminer. Le modèle devient
𝑑𝑆
𝑑𝑡
= 𝑟𝑆 &1 −
𝑆
𝐾
* − κ𝑆𝑇
𝑑𝑇
𝑑𝑡
= 𝑎𝑆 − 𝑑𝑇
où κ mesure la force des interactions anti-tumorales, 𝑎 dénote la croissance des cellules immunitaires
(proportionnelle au volume de la tumeur) et 𝑑 la mort de cellules immunitaires.
Écrivez un programme pour simuler ce dernier système. Prenez comme conditions initiales 𝑆(0) =
100 et 𝑇(0) = 0. Utilisez ce programme pour estimer les valeurs des paramètres 𝑟, 𝐾, 𝜅, 𝑎 et 𝑑 des
données fournies en estimant simultanément les données sans et avec traitement (notez que le
deuxième système se réduit à la première équation en posant 𝑇(0) = 0). Prenez les valeurs initiales
de 𝑟 = 1, 𝐾 = 1, 𝜅 = 0.0001, 𝑎 = 1 et 𝑑 = 1 pour les paramètres. Décrivez graphiquement les
dynamiques sans et avec traitement sur une période de 20 jours et fournissez un tableau des valeurs
des paramètres après l’estimation. Qu’advient-il à la tumeur au long terme après un traitement ?
2. L’algorithme de Gillespie nous permet de simuler un système réactionnel non-homogène ayant peu
de réactifs ou des réactions rares. En pseudo-code, l’algorithme consiste à
• initialiser la simulation pour un nombre initial de réactifs 𝑛4⃗ = 𝑛! et 𝑡 = 0
• échantillonner un chiffre aléatoire distribué uniformément entre 0 et 1
• calculer le temps d’attente τ par τ = −𝑙𝑜𝑔(𝑥")/𝑟
• échantillonner un deuxième chiffre aléatoire 𝑥# uniformément distribuer entre 0 et 1 pour
choisir la réaction qui aura lieu dans τ
• mettre à jour le temps, c’est-à-dire 𝑡 ⟶𝑡 + τ, et 𝑛4⃗ selon la réaction choisie et la matrice
stoechiométrique 𝑆
Nous pouvons également appliquer ce algorithme à des systèmes biologiques tels que des réseaux
de contrôle de l’expression génique. La synthèse de protéines commence par la transcription d’un
gène 𝐺 dans de l’acide ribonucléique messager (𝑚𝑅𝑁𝐴), une molécule intermédiaire à la protéine 𝑃.
Ce mRNA est ensuite transcrit pour synthétiser la protéine. L’autorégulation de ce processus se fait
par un dimère 𝐷 de la protéine, qui est généré spontanément de deux molécules 𝑃. Le dimère peut
aussi s’associer au gène pour bloquer la transcription (c’est-à-dire que l’expression génique est
réprimée). Le processus est complété par la dégradation du mRNA et de la protéine. Ce réseau
d’autorégulation est décrit par les processus :
transcription : G⟶G + mRNA
assemblage : mRNA⟶𝑚RNA + P
dimérisation : 2P ⟷𝐷
2
répression : G + D ⟷𝐷G
dégradation (mRNA) : mRNA ⟶∅
dégradation (protéine) : P ⟶∅
et les réactions suivantes :
r1 : 𝐺 + 𝑃# ⟹𝑃#𝐺
r2 : 𝑃#𝐺 ⟹𝐺 + 𝑃#
r3 : 𝐺 ⟹𝐺 + 𝑅
r4 : 𝑅 ⟹𝑅 + 𝑃
r5 : 2𝑃 ⟹𝑃#
r6 : 𝑃# ⟹2𝑃
r7 : 𝑅 ⟹∅
r8 : 𝑃 ⟹∅
où 𝑃# dénote une deuxième protéine intermédiaire. Écrivez un algorithme de Gillespie pour simuler
ces réactions en supposant que les réactions aient lieu aux taux suivants :
r1 = 1
r2 = 10
r3 = 0.01
r4 =10
r5 = 1
r6 =1
r7 = 0.1
r8 = 0.01
mesurés par secondes. Prenez comme condition initiale G = 10 avec toute autre population égale à 0
et Δ𝑡=0.01 comme pas de temps dans votre simulation. Tracer les graphiques des dynamiques sur un
maximum de 𝑡$%&=100 secondes (chaque simulation devrait prendre à peu près une minute). Tracer
des graphiques des dynamiques de chaque population pour une dizaine de réalisations de
l’algorithme. Le nombre d’essais est égale à 𝑡$'(/Δ𝑡. Tracez un histogramme de la probabilité d’une
réaction en fonction du nombre de molécules de protéines. Que pouvez-vous dire au sujet de
l’influence du nombre de protéines sur l’expression génique ? Qu’arrive-t-il aux dynamiques si
𝑡$%&=500 secondes ?
