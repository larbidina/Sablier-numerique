# ⏳ Sablier Numérique 

Projet 8 de mon apprentissage Arduino. Un sablier électronique : 6 LEDs 
s'allument une par une à intervalle régulier pour représenter le temps 
qui passe, et on réinitialise tout en retournant le montage, comme un 
vrai sablier qu'on retourne pour relancer le compte.

## Ce qu'il faut
- Arduino Uno
- 6 LEDs  + résistances
- 1 tilt sensor (capteur d'inclinaison)
- Breadboard + fils

## Le tilt sensor
C'est un petit composant qui contient une bille métallique à l'intérieur. 
Selon l'inclinaison, la bille touche ou non deux contacts internes, ce qui 
ferme ou ouvre le circuit, un peu comme un interrupteur, mais qui réagit 
à la position plutôt qu'à une pression. Ici il sert à détecter quand on 
retourne le sablier pour le réinitialiser.

## Comment ça marche
Toutes les minutes (réglable), une LED de plus s'allume, de la broche 2 
à la broche 7. Une fois les 6 LEDs allumées, il faut retourner le montage : 
le tilt sensor change d'état, toutes les LEDs s'éteignent, et le cycle 
recommence depuis le début.

## Ce que j'ai appris avec ce projet
- **`millis()`** : au lieu d'utiliser `delay()` qui bloque tout le programme, 
  `millis()` renvoie le temps écoulé depuis le démarrage de l'Arduino. 
  Ça permet de compter le temps entre deux LEDs tout en continuant à 
  vérifier l'état du capteur en même temps, sans rien bloquer.
- **`INPUT_PULLUP`** : ce mode active une résistance interne à l'Arduino 
  qui stabilise la lecture d'une entrée numérique (ici le tilt sensor). 
  Sans ça, la broche peut "flotter" électriquement et donner des lectures 
  instables. Avec `INPUT_PULLUP`, l'état lu est HIGH au repos et LOW 
  quand le circuit est fermé.
- **Boucle `for` pour initialiser plusieurs broches d'un coup** : plutôt 
  que d'écrire 6 fois `pinMode(x, OUTPUT)`, une seule boucle `for(int x = 2; x<8; x++)` 
  suffit pour configurer toutes les LEDs.

## Réglage du temps
long interval = 60000; // 1 minute entre chaque LED
