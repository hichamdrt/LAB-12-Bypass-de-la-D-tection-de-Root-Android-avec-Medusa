# LAB-12-Bypass-de-la-D-tection-de-Root-Android-avec-Medusa
# 🔐 LAB 12 — Analyse et contournement pédagogique de la détection Root Android avec Medusa

## Réalisé par

**Hamdi Maroua**

## Module

Sécurité des applications mobiles

## Environnement utilisé

* Windows PowerShell
* Android Studio Emulator (Pixel 5 API 30)
* ADB
* Frida
* Medusa

---

# 1. Présentation du laboratoire

Ce laboratoire a pour objectif d’étudier le mécanisme de détection du root Android et d’utiliser l’outil **Medusa** afin de réaliser un bypass dans un environnement de test contrôlé.

Medusa est un framework d’instrumentation dynamique reposant principalement sur **Frida**. Il permet d’interagir avec une application Android pendant son exécution afin d’analyser certains mécanismes de sécurité.

Dans ce lab, l’application cible est :

| Application         | Package                   |
| ------------------- | ------------------------- |
| Uncrackable Level 3 | `owasp_mstg_uncrackable3` |

L’objectif principal consiste à :

* lancer l’application dans un émulateur Android ;
* vérifier la communication avec ADB et Frida ;
* installer et configurer Medusa ;
* appliquer un module de bypass de détection root ;
* observer le comportement final de l’application.

---

# 2. Cadre éthique

Ce laboratoire est réalisé exclusivement dans un environnement pédagogique et autorisé.

Les techniques présentées doivent être utilisées uniquement :

* sur des applications de test ;
* dans des laboratoires d’apprentissage ;
* sur des systèmes disposant d’une autorisation explicite.

Le but du travail est de comprendre les mécanismes de sécurité mobile et d’évaluer leur robustesse dans un contexte académique.

---

# 3. Organisation des captures d’écran

Créer un dossier nommé :

```text id="p5w8x0"
images/
```


---

# 4. Capture 1 — Présentation générale du lab

La première capture présente la page principale du laboratoire intitulé :

<img width="255" height="308" alt="image" src="https://github.com/user-attachments/assets/f714a581-acad-44db-b9a2-bf73d7b0e739" />

## LAB 12 — Analyse et Bypass de la Détection Root Android avec Medusa

Elle montre :

* les objectifs du laboratoire ;
* les outils utilisés ;
* les étapes principales ;
* l’utilisation de Frida et Medusa ;
* la validation finale du bypass.

**Capture associée :** `pic1`

---

# 5. Capture 2 — Lancement de Medusa

<img width="1324" height="712" alt="image" src="https://github.com/user-attachments/assets/5eb11bfa-e0ae-4d66-980d-36887f28b8ae" />

Cette étape montre l’exécution de Medusa depuis Windows PowerShell.

Commande utilisée :

```bash id="2i8fdx"
python medusa.py -p owasp_mstg_uncrackable3 -r universal_root_detection_bypass
```

## Explication

| Paramètre                         | Description                                      |
| --------------------------------- | ------------------------------------------------ |
| `python medusa.py`                | Lance le framework Medusa                        |
| `-p`                              | Indique le package Android cible                 |
| `-r`                              | Charge un module ou une recette Medusa           |
| `universal_root_detection_bypass` | Module utilisé pour contourner la détection root |

Lors de l’exécution, Medusa détecte automatiquement les périphériques Android disponibles.

Exemple :

```text id="p4z6a1"
Android Emulator 5554
```

Cette étape confirme que Medusa communique correctement avec l’émulateur Android.

**Capture associée :** `pic2`

---

# 6. Capture 3 — Vérification de Frida

<img width="625" height="787" alt="image" src="https://github.com/user-attachments/assets/3b12ce84-c4d4-429a-9219-486306ff48a3" />


La commande suivante permet de vérifier la communication entre Frida et l’émulateur Android :

```bash id="h9u1r5"
frida-ps -U
```

Cette commande affiche les processus actifs détectés sur l’appareil Android connecté.

Parmi les processus visibles :

* Calendar ;
* Chrome ;
* Clock ;
* Settings ;
* adb ;
* adbd.

Cette vérification est importante car Medusa dépend directement de Frida pour réaliser l’instrumentation dynamique de l’application cible.

**Capture associée :** `pic3`

---

# 7. Capture 4 — Installation de Medusa et affichage de l’aide

<img width="685" height="791" alt="image" src="https://github.com/user-attachments/assets/4fb708b3-09a2-41d3-a04c-ffa0e1b7c8f1" />

## Installation de Medusa

```bash id="x0j7nd"
pip install medusa
```

Cette commande installe Medusa via le gestionnaire de paquets Python.

## Affichage de l’aide

```bash id="v4q2oe"
python medusa.py --help
```

L’aide affiche les principales options disponibles :

| Option                  | Fonction                      |
| ----------------------- | ----------------------------- |
| `-h` / `--help`         | Afficher l’aide               |
| `-r` / `--recipe`       | Charger un module             |
| `--not-interactive`     | Exécution sans interaction    |
| `-t` / `--time`         | Définir une durée d’exécution |
| `-p` / `--package-name` | Spécifier le package Android  |
| `-d` / `--device`       | Choisir un périphérique       |
| `-s` / `--save`         | Sauvegarder les logs          |

Cette étape confirme que Medusa est correctement installé et opérationnel.

**Capture associée :** `pic4`

---

# 8. Capture 5 — Application Android cible

<img width="248" height="428" alt="image" src="https://github.com/user-attachments/assets/a97d0c1c-ada9-4110-a495-6e169e8f4fec" />

Cette capture montre l’application **Uncrackable Level 3** lancée dans l’émulateur Android Pixel 5 API 30.

L’interface contient :

* un champ de saisie intitulé :

```text id="f5m2wa"
Enter the Secret String
```

* un bouton :

```text id="z6q9ep"
VERIFY
```

Cette application sert de cible pédagogique afin de tester les mécanismes de détection root Android.

**Capture associée :** `pic5`

---

# 9. Capture 6 — Validation du bypass

La dernière capture valide le fonctionnement du bypass de détection root.

Elle peut montrer :

* Medusa exécuté avec le module actif ;
* le terminal indiquant la sélection correcte du périphérique Android ;
* l’application fonctionnant normalement après bypass ;
* l’absence de blocage lié au root.

Cette étape confirme que le module Medusa a été appliqué avec succès.

**Capture associée :** `pic6`

---

# 10. Commandes utilisées

## Vérification de l’architecture CPU

```bash id="w0u8k1"
adb shell getprop ro.product.cpu.abi
```

### Résultat obtenu

```text id="n8b6fc"
x86_64
```

Cette commande affiche l’architecture processeur utilisée par l’émulateur Android.

---

## Vérification de Frida

```bash id="k3m5dv"
frida-ps -U
```

Permet de vérifier que Frida détecte correctement l’appareil Android.

---

## Installation de Medusa

```bash id="j4r8sy"
pip install medusa
```

Installe Medusa sur l’environnement Windows.

---

## Affichage de l’aide

```bash id="a7p1eh"
python medusa.py --help
```

Affiche les options disponibles dans Medusa.

---

## Lancement du bypass root

```bash id="m2x4tr"
python medusa.py -p owasp_mstg_uncrackable3 -r universal_root_detection_bypass
```

Exécute le module de bypass de détection root sur l’application cible.

---

# 11. Explication technique

Dans ce laboratoire, l’environnement Android a été préparé à l’aide d’un émulateur Pixel 5 API 30.

Les étapes suivantes ont ensuite été réalisées :

1. vérification de la connexion ADB ;
2. validation du fonctionnement de Frida ;
3. installation de Medusa ;
4. consultation des options disponibles ;
5. lancement du module de bypass root ;
6. observation du comportement de l’application Android.

Le module chargé dans Medusa permet d’intercepter certaines vérifications effectuées par l’application afin d’empêcher la détection du root.

---

# 12. Résultats obtenus

Le laboratoire a permis de :

* configurer un environnement Android de test ;
* vérifier la communication entre ADB, Frida et l’émulateur ;
* installer et exécuter Medusa ;
* appliquer un module de bypass root ;
* analyser le comportement de l’application après instrumentation dynamique.

---

# 13. Conclusion

Ce laboratoire montre comment les outils d’instrumentation dynamique peuvent être utilisés pour analyser les protections de sécurité mises en place dans une application Android.

L’association de Medusa et Frida permet d’étudier le comportement interne d’une application et d’évaluer la robustesse des mécanismes de détection root.

Toutes les manipulations réalisées dans ce laboratoire doivent rester limitées à un environnement pédagogique, contrôlé et autorisé.
