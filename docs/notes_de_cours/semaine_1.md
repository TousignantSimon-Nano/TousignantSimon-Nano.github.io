## Ligne du temps textuelle

### Années 1980
- **1982 – Intel 286 (80286)** : multitâche rudimentaire.
- **1985 – Intel 386 (80386)** : vrai 32 bits.
- **1989 – Intel 486 (80486)** : coprocesseur intégré.
- **1991 – AMD Am386** : premier processeur concurrentiel d’AMD.

### Années 1990
- **1993 – Intel Pentium** : référence du PC grand public.
- **1997 – Intel Pentium II / AMD K6** : guerre des performances.
- **1999 – Intel Pentium III / AMD Athlon (K7)** : AMD prend l’avantage.

### Années 2000
- **2000 – Intel Pentium 4 (NetBurst)** : fréquence brute, efficacité limitée.
- **2003 – AMD Athlon 64 (K8)** : première architecture 64 bits grand public.
- **2006 – Intel Core / Apple passe à Intel** : retour à l’efficacité.

### Années 2010
- **2008–2010 – Intel Core i3/i5/i7** : segmentation moderne.
- **2011 – AMD Bulldozer** : architecture critiquée.
- **2012 – Raspberry Pi 1 (ARM11)** : démocratisation des mini-PC ARM.
- **2015 – Raspberry Pi 2 (Cortex-A7)**  
- **2016 – Raspberry Pi 3 (Cortex-A53, 64 bits)**  
- **2017 – AMD Ryzen (Zen)** : retour en force.  
- **2019 – Raspberry Pi 4 (Cortex-A72)**  

### Années 2020 → Aujourd’hui
- **2020 – Apple M1 (ARM)** : rupture technologique.  
- **2023 – Raspberry Pi 5 (Cortex-A76) / Apple M3**.  

# Pourquoi ARM refait surface

L’architecture ARM, longtemps associée aux systèmes embarqués et aux smartphones, occupe aujourd’hui une place croissante dans des domaines où l’architecture **x86** (Intel, AMD) dominait jusqu’ici. Plusieurs facteurs expliquent cette montée en puissance.

---

## 1. Efficacité énergétique
Les processeurs ARM se distinguent par leur **faible consommation d’énergie**.  
Cette caractéristique, essentielle dans le mobile, devient également un atout majeur dans les ordinateurs portables et les centres de données, où autonomie et coûts énergétiques sont stratégiques.

---

## 2. Poids du marché mobile
Depuis l’iPhone (2007) et l’essor d’Android, ARM est devenu la base de tous les smartphones et tablettes.  
Cette adoption massive a généré un **écosystème mature** et des coûts de production compétitifs, rendant ARM attractif au-delà du mobile.

---

## 3. L’exemple d’Apple
Avec la sortie du **processeur Apple M1** en 2020, Apple a montré qu’un processeur ARM pouvait rivaliser avec, voire dépasser, des solutions x86 en termes de **puissance par watt**.  
L’autonomie accrue et les performances de cette nouvelle génération ont repositionné ARM dans l’informatique personnelle.

---

## 4. Intérêt croissant dans le cloud
Les grands acteurs du cloud, notamment **Amazon Web Services** avec ses puces **Graviton**, exploitent ARM pour réduire la consommation électrique et optimiser les coûts d’exploitation des datacenters.

---

## 5. Flexibilité de conception
Contrairement à Intel et AMD, ARM ne produit pas directement de processeurs : il **licencie son architecture**.  
Cela permet à différents acteurs (Apple, Qualcomm, Nvidia, etc.) de concevoir leurs propres variantes, adaptées à des usages spécifiques, du smartphone au serveur haute performance.

---

## Conclusion
Le retour en force d’ARM s’explique par la convergence de plusieurs tendances :
- l’importance croissante de l’efficacité énergétique,  
- l’expérience acquise grâce au marché mobile,  
- la démonstration de sa viabilité sur desktop (Apple Silicon),  
- et l’intérêt stratégique des grands acteurs du cloud.  

ARM n’est donc plus limité aux systèmes embarqués : il devient une **alternative sérieuse à x86** dans les ordinateurs, les serveurs et les infrastructures modernes.
  
  
# Raspberry Pi : Histoire et Impact

---

## 📍 Position dans la ligne du temps

- **2012 – Raspberry Pi 1 (ARM11, 700 MHz)** : lancement par la Raspberry Pi Foundation au Royaume-Uni.  
- Il arrive **après la vague PC Intel/AMD** (1980–2000), **en parallèle du boom mobile ARM** (smartphones), et **avant l’émergence d’Apple Silicon**.  
- Il s’inscrit dans la continuité de la **miniaturisation et de la démocratisation de l’informatique**.

---

## 🎯 Motivations initiales

- **Éducation** : créer un ordinateur ultra-abordable pour initier les enfants à la programmation.  
- **Accessibilité** : rendre l’informatique et l’électronique abordables, notamment dans les pays en développement.  
- **Expérimentation** : offrir une plateforme simple et flexible aux makers, hobbyistes et chercheurs.

---

## ✅ Gains et apports

- **Coût extrêmement bas** : un ordinateur complet dès 35 USD. (Jadis)  
- **Économie d’énergie** : architecture ARM très peu gourmande, utilisable sur batterie ou alimentation légère.  
- **Polyvalence** : PC basique, serveur, contrôleur domotique, outil pédagogique, support pour projets IoT/robotique…  
- **Écosystème logiciel riche** : compatible Linux, Python, et de nombreuses bibliothèques éducatives.  
- **Accessibilité mondiale** : des millions de personnes ont ainsi pu avoir un premier contact concret avec la programmation et l’informatique physique.

---

## 🌍 Engouement et impact

- **Communauté mondiale** : développeurs, enseignants, makers, entreprises.  
- **Adoption en éducation** : utilisé dans écoles et universités comme support d’apprentissage.  
- **Culture maker** : devenu un symbole du DIY et de la créativité technologique.  
- **Applications professionnelles** : prototypes industriels, bornes interactives, objets connectés, serveurs légers.  
- **Symbole de démocratisation** : a montré qu’un ordinateur pouvait être accessible à tous, à l’image des micro-ordinateurs des années 1980.

---

## 📌 En résumé

L’arrivée du Raspberry Pi marque un **tournant culturel** dans l’informatique :  

- après l’ère des processeurs de performance (Intel/AMD),  
- au cœur de l’essor ARM sur mobile,  
- il a incarné **la démocratisation de l’informatique ouverte, éducative et accessible**.  

Moins une révolution technologique qu’une **révolution dans l’usage et l’appropriation des processeurs ARM**, le Raspberry Pi a profondément changé la manière dont on explore et utilise l’informatique au quotidien.

# RISC vs CISC : Comprendre les architectures de processeur

RISC (**Processeur à jeu d’instructions réduit**) et CISC (**Processeur à jeu d’instructions complexe**) représentent deux philosophies de conception des processeurs. Elles définissent **comment un processeur exécute les instructions**.

---

## 1️⃣ CISC – Processeur à jeu d’instructions complexe

- **Principe** : disposer d’un **grand nombre d’instructions complexes**, certaines pouvant effectuer plusieurs opérations en une seule commande.  
- **Avantage** : le code peut être plus compact et parfois plus simple à programmer en langage machine.  
- **Inconvénient** : le processeur est plus complexe, consomme plus d’énergie, dégage plus de chaleur et le traitement en pipeline peut être moins efficace.  
- **Exemple** : les processeurs Intel et AMD de la famille x86. Ces processeurs peuvent charger, calculer et stocker en une seule instruction.

---

## 2️⃣ RISC – Processeur à jeu d’instructions réduit

- **Principe** : utiliser un **jeu d’instructions simple et uniforme**, chaque instruction effectuant **une seule opération élémentaire**.  
- **Avantage** : architecture plus simple, traitement en pipeline plus efficace, fréquence plus élevée, faible consommation. Idéal pour les appareils mobiles et embarqués.  
- **Inconvénient** : le code peut être plus long car il faut combiner plusieurs instructions simples pour effectuer le même travail qu’une instruction CISC.  
- **Exemple** : ARM (Raspberry Pi, smartphones), MIPS, RISC-V.

---

## ⚖️ Comparaison directe

| Critère | CISC | RISC |
|---------|------|------|
| Nombre d’instructions | Nombreuses et complexes | Peu nombreuses et simples |
| Taille du code | Compact | Plus long |
| Complexité du processeur | Élevée | Faible |
| Pipeline / vitesse | Moins efficace | Très efficace |
| Consommation d’énergie | Élevée | Faible |
| Exemple | Intel x86, AMD | ARM, MIPS, RISC-V |

---

## 💡 Importance actuelle

- Les **processeurs modernes x86** restent CISC “en apparence”, mais utilisent des techniques internes proches du RISC pour optimiser le traitement.  
- Les **processeurs ARM** sont RISC et dominent le marché mobile grâce à leur faible consommation et leur efficacité.  
- RISC est aujourd’hui privilégié dans les **objets connectés, smartphones, Raspberry Pi et Apple Silicon**.