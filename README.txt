# Halite Bot - PA 2022 Project

# Echipa: hardcoded_success_overflow

# Membri: Bala Alexandru-Constantin, 323CC - capitan
          Buhnici Andrei-George, 323CC
          Ripanu Catalin-Alexandru, 323CC

I) instructiuni de compilare

- Compilarea se face din linia de comanda, folosind Makefile-ul, iar header-ele
  si sursele se afla in folder-ul sources.

II) Detalii despre structura proiectului

1) Proiectul contine urmatoarele headere:
-> hlt.hpp
-> networking.hpp
-> Robot.hpp

2) Proiectul contine urmatoarele surse:
-> Robot.cpp
-> myBot.cpp

3) De asemenea, proiectul contine un Makefile cu regulile cerute de:
-> build 
-> clean
-> run

III) Detalii de implementare

1) Implementarea efectiva a bot-ului este facuta in clasa Robot. Botul aplica
   strategia urmatoare:

- Casutele din interiorul terenului ocupat vor cauta cea mai apropiata granita,
  iar daca aceasta nu exista se va sta pe loc.
- Casutele de la granita folosesc o abordare greedy pentru a ataca piesele inca
  neocupate. Astfel, o piesa va ataca imediat ce este posibil, iar daca exista
  mai multe astfel de casute ce pot fi atacate, atunci va fi aleasa piesa cu 
  cel mai mare scor.
- Daca o casuta de la granita nu poate ataca, atunci ea va cauta o casuta 
  vecina de la granita cu care poate sa se combine, fara a face OVERFLOW. 
  Pentru aceasta, este tinuta o matrice cu puterile casutelor (strength_map).
- Dupa modelul de la link-urile [2] si [3], casutele de granita prioritizeaza 
  acum casutele cele mai vulnerabile ale inamicului.
- Pentru deadline-ul final am schimbat functia de save_strength pentru o 
  euristica mai buna :
  -> Combina Greedy cu DP.
  -> Ideea principala este ca, tot pentru celule de 255 strength, nu se uita doar 
  la mutarea curenta, si se uita si la urmatoarea celula incercand sa redirecteze cat 
  mai bine puterea in exces pentru a ajuta o parte cat mai mare din celulele din jurul sau.
  Fie pentru a cuceri o celula neutra sau fie pentru una inamica. Pentru cea inamica se 
  uita inclusiv la o locatie dupa prima celula inamica pentru a transfera si mai multa
  putere. Si cat timp este inca la putere maxima se va tot redirectiona putere. Am pus
  accent pe partea ofensiva, in sensul ca prioretizam celulele care se lupta.

2) Complexitatea:

- Se noteaza cu width lungimea tabelei si cu height latimea tabelei
- Realizarea unei mutari se va face in timp constant O(1) pentru casutele
  de la granita (exterioare), iar pentru o casuta interioara se va face in 
  O(height) 
- Corectia puterii ramane tot O((width * height) ^ 2).
- Deci, complexitatea totala a algoritmului folosit va fi determinata de
  corectia puterii (care este cea mai mare), adica O((width * height) ^ 2).

IV) Surse de inspiratie

1) Am pornit implementarea de la tutorialele de pe site-ul jocului si de pe 
   forum-uri:
[1] - https://2017.halite.io/learn-programming-challenge/downloads-and-starter-kits/improve-basic-bot
[2] - https://2016.forums.halite.io/t/so-youve-improved-the-random-bot-now-what/482.html
[3] - https://2016.forums.halite.io/t/published-bot-source-code/987.html

2) In plus, am analizat si strategiile folosite de alti jucatori din cadrul 
   proiectului:
[4] - https://pa.readerbench.com/

V) Responsabilitatea fiecarui membru al echipei

Design (coding style si README) -> Bala Alexandru-Constantin
Research & Strategie -> Toata echipa
Algoritmul utilizat -> Toata echipa
Implementarea algoritmului -> Buhnici Andrei-George & Ripanu-Catalin Alexandru
