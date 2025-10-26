# Partie 8.1 : Jeux et Applications

## 🎯 Objectifs Pédagogiques

Ce chapitre présente des **projets de jeux et applications** complets, combinant tous les concepts appris dans les parties précédentes pour créer des programmes interactifs et divertissants.

### Concepts Intégrés
- **Jeux classiques** : pendu, devinette, score
- **Logique de jeu** : boucles, conditions, interfaces
- **Applications pratiques** : simulations, interfaces utilisateur
- **Fonctionnalités** : sauvegarde, scores, replay

---

## 📝 Exercices Pratiques

### Exercice 286 : Jeu du pendu complet
**Objectif** : Implémenter le jeu du pendu avec interface complète.

```python
# Solution
import random

def jeu_du_pendu():
    """Jeu du pendu complet"""
    # Liste de mots
    mots = ["python", "programmation", "ordinateur", "algorithme", "variable", "fonction", "classe", "objet"]

    # Sélection aléatoire d'un mot
    mot_secret = random.choice(mots).upper()
    lettres_trouvees = set()
    tentatives_max = 6
    tentatives = 0
    lettres_proposees = set()

    print("🎯 JEU DU PENDU 🎯")
    print(f"Mot de {len(mot_secret)} lettres à deviner")
    print("Vous avez 6 tentatives")

    while tentatives < tentatives_max:
        # Affichage du mot masqué
        mot_affiche = ""
        for lettre in mot_secret:
            if lettre in lettres_trouvees:
                mot_affiche += lettre + " "
            else:
                mot_affiche += "_ "

        print(f"\nMot : {mot_affiche}")
        print(f"Tentatives restantes : {tentatives_max - tentatives}")

        # Saisie de l'utilisateur
        while True:
            lettre = input("Proposez une lettre : ").upper()
            if len(lettre) == 1 and lettre.isalpha():
                break
            print("Veuillez entrer une seule lettre.")

        # Vérification lettre déjà proposée
        if lettre in lettres_proposees:
            print(f"Lettre '{lettre}' déjà proposée")
            continue

        lettres_proposees.add(lettre)

        # Test de la lettre
        if lettre in mot_secret:
            lettres_trouvees.add(lettre)
            print(f"✓ Bonne lettre : '{lettre}'")

            # Vérification si mot complet
            if all(lettre in lettres_trouvees for lettre in mot_secret):
                print(f"\n🎉 BRAVO ! Mot trouvé : {mot_secret}")
                print(f"Tentatives utilisées : {tentatives + 1}")
                return True
        else:
            tentatives += 1
            print(f"❌ Lettre incorrecte : '{lettre}'")

            # Affichage du pendu
            afficher_pendu(tentatives)

    # Échec
    print(f"\n💀 PERDU ! Le mot était : {mot_secret}")
    return False

def afficher_pendu(etape):
    """Affiche l'état du pendu"""
    etapes = [
        """
         +---+
         |   |
             |
             |
             |
             |
        =========
        """,
        """
         +---+
         |   |
         O   |
             |
             |
             |
        =========
        """,
        """
         +---+
         |   |
         O   |
         |   |
             |
             |
        =========
        """,
        """
         +---+
         |   |
         O   |
        /|   |
             |
             |
        =========
        """,
        """
         +---+
         |   |
         O   |
        /|\\  |
             |
             |
        =========
        """,
        """
         +---+
         |   |
         O   |
        /|\\  |
        /    |
             |
        =========
        """,
        """
         +---+
         |   |
         O   |
        /|\\  |
        / \\  |
             |
        =========
        """
    ]

    print(etapes[etape])

# Test
print("=== JEU DU PENDU ===")
jouer = input("Voulez-vous jouer ? (o/n) : ").lower()
if jouer == 'o':
    jeu_du_pendu()

    # Rejouer ?
    while True:
        rejouer = input("Voulez-vous rejouer ? (o/n) : ").lower()
        if rejouer == 'o':
            jeu_du_pendu()
        else:
            print("Merci d'avoir joué !")
            break
else:
    print("Au revoir !")
```

**Explication** :
- **Jeu complet** : interface, logique, affichage
- **ASCII art** : pendu progressif
- **Gestion d'erreurs** : lettres déjà proposées
- **Victoire/échec** : conditions de fin
- **Rejouabilité** : boucle de jeu

**Test** : Jouez au pendu et essayez de deviner le mot.

---

### Exercice 287 : Mini moteur de Scrabble
**Objectif** : Implémenter un système de calcul de score Scrabble.

```python
# Solution
def calculer_score_scrabble(mot):
    """Calcule le score Scrabble d'un mot"""
    # Table de scores Scrabble (lettres majuscules)
    scores = {
        'A': 1, 'B': 3, 'C': 3, 'D': 2, 'E': 1, 'F': 4, 'G': 2, 'H': 4, 'I': 1,
        'J': 8, 'K': 5, 'L': 1, 'M': 3, 'N': 1, 'O': 1, 'P': 3, 'Q': 10, 'R': 1,
        'S': 1, 'T': 1, 'U': 1, 'V': 4, 'W': 4, 'X': 8, 'Y': 4, 'Z': 10
    }

    mot = mot.upper()
    score = 0

    for lettre in mot:
        if lettre.isalpha():
            score += scores.get(lettre, 0)
        else:
            print(f"Lettre invalide ignorée : '{lettre}'")

    return score

def comparer_mots_scrabble(mots):
    """Compare les scores de plusieurs mots"""
    scores = {}

    for mot in mots:
        score = calculer_score_scrabble(mot)
        scores[mot] = score
        print(f"'{mot}' : {score} points")

    # Mot avec le meilleur score
    if scores:
        meilleur_mot = max(scores, key=scores.get)
        print(f"\n🏆 Meilleur mot : '{meilleur_mot}' ({scores[meilleur_mot]} points)")
        return scores
    return {}

# Test
print("=== CALCULATEUR SCRABBLE ===")

mots_test = ["PYTHON", "PROGRAMMATION", "ALGORITHME", "VARIABLE", "FONCTION"]
print("Scores des mots de programmation :")
scores = comparer_mots_scrabble(mots_test)

# Test avec saisie utilisateur
while True:
    mot = input("\nEntrez un mot (ou 'quit' pour arrêter) : ").strip()
    if mot.lower() == 'quit':
        break

    if mot:
        score = calculer_score_scrabble(mot)
        print(f"Score de '{mot}' : {score} points")

print("Merci d'avoir utilisé le calculateur Scrabble !")
```

**Explication** :
- **Scores officiels** : table Scrabble complète
- **Gestion erreurs** : lettres invalides
- **Comparaison** : classement des mots
- **Interface interactive** : saisie continue

**Test** : Calculez les scores de différents mots.

---

### Exercice 288 : Mini jeu de devinette avec score
**Objectif** : Créer un jeu de devinette avec système de score.

```python
# Solution
import random

class JeuDevinette:
    """Jeu de devinette avec système de score"""

    def __init__(self):
        self.score = 0
        self.parties_jouees = 0
        self.meilleur_score = 0

    def nouvelle_partie(self):
        """Démarre une nouvelle partie"""
        self.nombre_secret = random.randint(1, 100)
        self.tentatives = 0
        self.parties_jouees += 1

        print("
🎲 NOUVELLE PARTIE 🎲"        print(f"Partie n°{self.parties_jouees}")
        print("Devinez le nombre entre 1 et 100")

    def faire_tentative(self, guess):
        """Traite une tentative"""
        self.tentatives += 1

        if guess < self.nombre_secret:
            print("📈 Trop petit !")
            return False
        elif guess > self.nombre_secret:
            print("📉 Trop grand !")
            return False
        else:
            # Victoire
            points = max(100 - self.tentatives * 10, 10)  # Score basé sur tentatives
            self.score += points
            if self.score > self.meilleur_score:
                self.meilleur_score = self.score

            print(f"🎉 Bravo ! Trouvé en {self.tentatives} tentatives")
            print(f"Points gagnés : {points}")
            print(f"Score actuel : {self.score}")
            return True

    def afficher_stats(self):
        """Affiche les statistiques"""
        print("
📊 STATISTIQUES 📊"        print(f"Parties jouées : {self.parties_jouees}")
        print(f"Score total : {self.score}")
        print(f"Meilleur score : {self.meilleur_score}")
        if self.parties_jouees > 0:
            print(f"Moyenne par partie : {self.score / self.parties_jouees:.1f}")

    def jouer(self):
        """Lance le jeu principal"""
        print("🎯 JEU DE DEVINETTE AVEC SCORE 🎯")

        while True:
            self.nouvelle_partie()

            while True:
                try:
                    guess = int(input("Votre proposition : "))
                    if 1 <= guess <= 100:
                        break
                    else:
                        print("Entrez un nombre entre 1 et 100")
                except ValueError:
                    print("Entrez un nombre valide")

            if self.faire_tentative(guess):
                break

            # Limite de tentatives
            if self.tentatives >= 10:
                print(f"❌ Trop de tentatives ! Le nombre était {self.nombre_secret}")
                break

        self.afficher_stats()

# Test
if __name__ == "__main__":
    jeu = JeuDevinette()
    jeu.jouer()
```

**Explication** :
- **Classe de jeu** : encapsulation complète
- **Système de score** : points basés sur tentatives
- **Statistiques** : suivi des performances
- **Interface** : saisie et feedback
- **Limites** : nombre de tentatives maximum

**Test** : Jouez au jeu de devinette et améliorez votre score.

---

### Exercice 289 : Simulation de tirage aléatoire
**Objectif** : Simuler des tirages aléatoires avec analyse statistique.

```python
# Solution
import random

def simulation_tirage(nb_simulations=1000, nb_faces=6):
    """Simule des tirages de dé"""
    resultats = []

    print(f"🎲 SIMULATION DE {nb_simulations} TIRAGES DE DÉ À {nb_faces} FACES 🎲")

    for i in range(nb_simulations):
        tirage = random.randint(1, nb_faces)
        resultats.append(tirage)

        # Affichage progressif (tous les 100 tirages)
        if (i + 1) % 100 == 0:
            print(f"Tirage {i + 1}/{nb_simulations} : {tirage}")

    # Analyse des résultats
    from collections import Counter

    frequences = Counter(resultats)
    total = len(resultats)

    print("
📊 ANALYSE STATISTIQUE 📊"    print(f"Nombre de simulations : {total}")
    print(f"Nombre de faces : {nb_faces}")
    print(f"Probabilité théorique par face : {1/nb_faces:.3f}")

    print("
Résultats observés :"    for face in range(1, nb_faces + 1):
        freq = frequences.get(face, 0)
        proba_observe = freq / total
        ecart = abs(proba_observe - 1/nb_faces) / (1/nb_faces) * 100

        print(f"Face {face}: {freq"4d"} fois ({proba_observe".3f"}) - Écart: {ecart"5.1f"}%")

    # Face la plus fréquente
    face_plus_freq = frequences.most_common(1)[0]
    print(f"\n🏆 Face la plus fréquente : {face_plus_freq[0]} ({face_plus_freq[1]} fois)")

    return resultats

# Test
resultats = simulation_tirage(10000, 6)
```

**Explication** :
- **Simulation** : tirages aléatoires multiples
- **Analyse statistique** : fréquences observées
- **Comparaison** : avec probabilités théoriques
- **Visualisation** : affichage progressif
- **Applications** : théorie des probabilités

**Test** : Simulez des milliers de tirages et analysez les résultats.

---

### Exercice 290 : Mini jeu de devinette avec score
**Objectif** : Étendre le jeu de devinette avec un système de score.

```python
# Solution - Version étendue du jeu de devinette
class JeuDevinetteAvance:
    """Jeu de devinette avec système de score avancé"""

    def __init__(self):
        self.score = 0
        self.parties_jouees = 0
        self.parties_gagnees = 0
        self.meilleur_score = 0
        self.historique = []

    def calculer_points(self, tentatives):
        """Calcule les points selon les tentatives"""
        return max(100 - tentatives * 5, 0)

    def nouvelle_partie(self, difficulte="moyen"):
        """Démarre une nouvelle partie"""
        # Configuration selon difficulté
        if difficulte == "facile":
            self.plage = (1, 50)
            self.tentatives_max = 10
        elif difficulte == "difficile":
            self.plage = (1, 200)
            self.tentatives_max = 8
        else:  # moyen
            self.plage = (1, 100)
            self.tentatives_max = 7

        self.nombre_secret = random.randint(self.plage[0], self.plage[1])
        self.tentatives = 0
        self.parties_jouees += 1

        print(f"\n🎯 PARTIE {self.parties_jouees} - DIFFICULTÉ: {difficulte.upper()} 🎯")
        print(f"Nombre entre {self.plage[0]} et {self.plage[1]}")
        print(f"Tentatives maximum : {self.tentatives_max}")

    def faire_tentative(self, guess):
        """Traite une tentative"""
        if not (self.plage[0] <= guess <= self.plage[1]):
            print(f"Veuillez entrer un nombre entre {self.plage[0]} et {self.plage[1]}")
            return False

        self.tentatives += 1

        if guess < self.nombre_secret:
            print("📈 Trop petit !"            if self.tentatives < self.tentatives_max:
                print(f"Il vous reste {self.tentatives_max - self.tentatives} tentatives")
            return False
        elif guess > self.nombre_secret:
            print("📉 Trop grand !"            if self.tentatives < self.tentatives_max:
                print(f"Il vous reste {self.tentatives_max - self.tentatives} tentatives")
            return False
        else:
            # Victoire
            points = self.calculer_points(self.tentatives)
            self.score += points
            self.parties_gagnees += 1

            if self.score > self.meilleur_score:
                self.meilleur_score = self.score

            # Sauvegarde dans l'historique
            self.historique.append({
                "partie": self.parties_jouees,
                "tentatives": self.tentatives,
                "points": points,
                "gagnee": True
            })

            print(f"🎉 BRAVO ! Trouvé en {self.tentatives} tentatives")
            print(f"Points gagnés : {points}")
            print(f"Score actuel : {self.score}")
            return True

    def abandonner(self):
        """Abandonne la partie"""
        self.historique.append({
            "partie": self.parties_jouees,
            "tentatives": self.tentatives,
            "points": 0,
            "gagnee": False
        })
        print(f"💔 Abandon ! Le nombre était {self.nombre_secret}")

    def afficher_stats(self):
        """Affiche les statistiques détaillées"""
        print("
📊 STATISTIQUES DÉTAILLÉES 📊"        print(f"Parties jouées : {self.parties_jouees}")
        print(f"Parties gagnées : {self.parties_gagnees}")
        if self.parties_jouees > 0:
            print(f"Taux de réussite : {self.parties_gagnees / self.parties_jouees * 100:.1f}%")
        print(f"Score total : {self.score}")
        print(f"Meilleur score : {self.meilleur_score}")

        if self.historique:
            print("
Historique des 5 dernières parties :")
            for partie in self.historique[-5:]:
                statut = "✓" if partie["gagnee"] else "✗"
                print(f"  Partie {partie['partie']}: {partie['tentatives']} tentatives, {partie['points']} points {statut}")

    def menu_principal(self):
        """Affiche le menu principal"""
        print("🎯 MENU DU JEU DE DEVINETTE 🎯")
        print("1. Nouvelle partie (Facile)")
        print("2. Nouvelle partie (Moyen)")
        print("3. Nouvelle partie (Difficile)")
        print("4. Afficher statistiques")
        print("5. Quitter")

    def jouer(self):
        """Lance le jeu principal"""
        print("🎯 JEU DE DEVINETTE AVANCÉ 🎯")

        while True:
            self.menu_principal()
            choix = input("Votre choix (1-5) : ").strip()

            if choix == "1":
                self.nouvelle_partie("facile")
                self.jouer_partie()
            elif choix == "2":
                self.nouvelle_partie("moyen")
                self.jouer_partie()
            elif choix == "3":
                self.nouvelle_partie("difficile")
                self.jouer_partie()
            elif choix == "4":
                self.afficher_stats()
            elif choix == "5":
                print("Merci d'avoir joué !")
                break
            else:
                print("Choix invalide. Essayez 1-5.")

    def jouer_partie(self):
        """Joue une partie complète"""
        while self.tentatives < self.tentatives_max:
            try:
                guess = int(input("Votre proposition : "))
                if self.faire_tentative(guess):
                    break
            except ValueError:
                print("Entrez un nombre valide.")

        if self.tentatives >= self.tentatives_max:
            self.abandonner()

# Test
if __name__ == "__main__":
    jeu = JeuDevinetteAvance()
    jeu.jouer()
```

**Explication** :
- **Niveaux de difficulté** : plages et tentatives différentes
- **Menu interactif** : navigation dans le jeu
- **Historique** : suivi des parties
- **Statistiques détaillées** : taux de réussite, etc.
- **Abandon** : possibilité de quitter une partie

**Test** : Jouez avec différents niveaux de difficulté.

---

## 🔍 Points Clés à Retenir

### 1. **Structure de Jeu**
```python
class Jeu:
    def __init__(self):
        self.score = 0
        self.parties = 0

    def nouvelle_partie(self):
        # Logique de démarrage
        pass

    def faire_tentative(self, guess):
        # Logique de jeu
        pass

    def afficher_stats(self):
        # Affichage des statistiques
        pass
```

### 2. **Interface Utilisateur**
```python
def menu():
    print("1. Jouer")
    print("2. Statistiques")
    print("3. Quitter")
    choix = input("Votre choix : ")
    return choix

while True:
    choix = menu()
    if choix == "1":
        jouer()
    elif choix == "2":
        afficher_stats()
    elif choix == "3":
        break
```

### 3. **Gestion d'Erreurs**
```python
try:
    guess = int(input("Nombre : "))
except ValueError:
    print("Entrez un nombre valide")
    continue
```

### 4. **ASCII Art**
```python
def afficher_pendu(etape):
    etapes = ["""
     +---+
     |   |
         |
         |
         |
         |
    =========
    """, # ... autres étapes
    ]
    print(etapes[etape])
```

## 💡 Optimisations et Astuces

### 1. **Sauvegarde de Score**
```python
import json

def sauvegarder_score(score):
    try:
        with open("scores.json", "r") as f:
            scores = json.load(f)
    except:
        scores = []

    scores.append(score)
    with open("scores.json", "w") as f:
        json.dump(scores, f)
```

### 2. **Interface Graphique Simple**
```python
def afficher_interface(titre, options):
    print(f"\n=== {titre} ===")
    for i, option in enumerate(options, 1):
        print(f"{i}. {option}")
    return input("Votre choix : ")
```

### 3. **Multijoueur**
```python
def mode_multijoueur():
    joueurs = []
    for i in range(2):
        nom = input(f"Nom du joueur {i+1} : ")
        joueurs.append({"nom": nom, "score": 0})
    # Logique multijoueur
```

## 🚀 Applications Pratiques

### 1. **Jeu de Memory**
```python
class JeuMemory:
    """Jeu de memory avec cartes"""

    def __init__(self, taille=4):
        self.taille = taille
        self.cartes = self.generer_cartes()
        self.cartes_melangees = self.melanger_cartes()
        self.trouvees = set()

    def generer_cartes(self):
        """Génère les paires de cartes"""
        symboles = ["A", "B", "C", "D", "E", "F", "G", "H"]
        cartes = []
        for i in range(self.taille * self.taille // 2):
            cartes.extend([symboles[i], symboles[i]])
        return cartes

    def melanger_cartes(self):
        """Mélange les cartes"""
        import random
        cartes_melangees = self.cartes[:]
        random.shuffle(cartes_melangees)
        return cartes_melangees

    def afficher_grille(self):
        """Affiche la grille de jeu"""
        print("\nGrille de Memory :")
        for i in range(self.taille):
            ligne = ""
            for j in range(self.taille):
                index = i * self.taille + j
                if index in self.trouvees:
                    ligne += f" {self.cartes_melangees[index]} "
                else:
                    ligne += " ? "
            print(ligne)

    def jouer(self):
        """Lance le jeu"""
        print("🎯 JEU DE MEMORY 🎯")
        print("Retrouvez toutes les paires !")

        while len(self.trouvees) < len(self.cartes):
            self.afficher_grille()

            try:
                pos1 = int(input("Position 1 (0-15) : "))
                pos2 = int(input("Position 2 (0-15) : "))

                if pos1 == pos2:
                    print("Choisissez deux positions différentes")
                    continue

                if (pos1 not in range(len(self.cartes)) or
                    pos2 not in range(len(self.cartes))):
                    print("Positions invalides")
                    continue

                # Révélation des cartes
                carte1 = self.cartes_melangees[pos1]
                carte2 = self.cartes_melangees[pos2]

                print(f"Carte 1 : {carte1}")
                print(f"Carte 2 : {carte2}")

                if carte1 == carte2:
                    print("✓ Paire trouvée !")
                    self.trouvees.add(pos1)
                    self.trouvees.add(pos2)
                else:
                    print("❌ Pas une paire")

                input("Appuyez sur Entrée pour continuer...")

            except ValueError:
                print("Entrez des nombres valides")

        print("🎉 Félicitations ! Toutes les paires trouvées !")

# Test
memory = JeuMemory(4)  # Grille 4x4
memory.jouer()
```

### 2. **Simulateur de Dés**
```python
def simulateur_des_avance():
    """Simulateur de dés avec options"""
    print("🎲 SIMULATEUR DE DÉS AVANCÉ 🎲")

    # Configuration
    nb_des = int(input("Nombre de dés : "))
    nb_faces = int(input("Nombre de faces par dé : "))
    nb_lancers = int(input("Nombre de lancers : "))

    # Simulation
    resultats = []
    for _ in range(nb_lancers):
        lancer = sum(random.randint(1, nb_faces) for _ in range(nb_des))
        resultats.append(lancer)

    # Analyse
    from collections import Counter
    frequences = Counter(resultats)

    print("
Résultats de simulation :"    print(f"Total de lancers : {nb_lancers}")
    print(f"Minimum : {min(resultats)}")
    print(f"Maximum : {max(resultats)}")
    print(f"Moyenne : {sum(resultats) / len(resultats):.2f}")

    # Distribution
    print("
Distribution des sommes :")
    for somme in sorted(frequences.keys()):
        freq = frequences[somme]
        pourcentage = (freq / nb_lancers) * 100
        print(f"Somme {somme}: {freq"3d"} fois ({pourcentage"5.2f"}%)")

    return resultats

# Test
resultats = simulateur_des_avance()
```

### 3. **Quiz de Culture Générale**
```python
class Quiz:
    """Quiz de culture générale"""

    def __init__(self):
        self.questions = {
            "Quelle est la capitale de la France ?": "Paris",
            "Combien de continents y a-t-il ?": "7",
            "Quel est le plus grand océan ?": "Pacifique",
            "Qui a peint la Joconde ?": "Léonard de Vinci",
            "En quelle année l'homme a-t-il marché sur la Lune ?": "1969"
        }
        self.score = 0

    def poser_question(self, question, reponse_correcte):
        """Pose une question"""
        print(f"\nQuestion : {question}")
        reponse = input("Votre réponse : ").strip()

        if reponse.lower() == reponse_correcte.lower():
            print("✓ Correct !")
            self.score += 1
            return True
        else:
            print(f"❌ Incorrect. La réponse était : {reponse_correcte}")
            return False

    def jouer(self):
        """Lance le quiz"""
        print("🎓 QUIZ DE CULTURE GÉNÉRALE 🎓")
        print(f"{len(self.questions)} questions")

        for question, reponse in self.questions.items():
            self.poser_question(question, reponse)

        # Résultats
        print("
=== RÉSULTATS ==="        print(f"Score : {self.score}/{len(self.questions)}")
        pourcentage = (self.score / len(self.questions)) * 100
        print(f"Pourcentage : {pourcentage:.1f}%")

        if pourcentage >= 80:
            print("🏆 Excellent !")
        elif pourcentage >= 60:
            print("👍 Bien !")
        elif pourcentage >= 40:
            print("😐 Moyen")
        else:
            print("💪 À réviser !")

# Test
quiz = Quiz()
quiz.jouer()
```

## 🎯 Défis Supplémentaires

1. **Créez** un jeu de Pierre-Feuille-Ciseaux avec interface
2. **Implémentez** un générateur de mots croisés simple
3. **Développez** un simulateur de bataille navale
4. **Concevez** un système de classement pour les jeux

---

**Exercices complétés : 290/300** 🎯

*Continuez avec le [chapitre suivant](8-2-validation.md) pour la validation et parsing !*
