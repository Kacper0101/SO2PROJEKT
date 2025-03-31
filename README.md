# Problem Ucztujących Filozofów - Implementacja w C++



## 📖 Opis problemu
Problem ucztujących filozofów to klasyczny przykład w programowaniu współbieżnym ilustrujący wyzwania synchronizacji wątków i zarządzania zasobami. Pięciu filozofów siedzi przy okrągłym stole, każdy ma przed sobą talerz, a między nimi po jednym widelcu. Filozofowie na przemian myślą i jedzą, ale aby jeść, potrzebują dwóch widelców (lewego i prawego). Problem ilustruje wyzwania deadlocku, zagłodzenia i współdzielenia zasobów.
## 🛠 Wymagania
- Kompilator C++11 (g++/clang++)
- Biblioteka pthread
- System: Windows/Linux/macOS

## 🚀 Instalacja i uruchomienie

### Kompilacja
```
g++ -std=c++11 -pthread philosophers.cpp -o philosophers
```
### Uruchomienie 
```
  ./philosophers [liczba_filozofów]   (uruchomienie programu) 
 ./philosophers 5    (przykład) 
```
## 🏗 Architektura rozwiązania
# Główne komponenty
- CustomMutex - własna implementacja mechanizmu blokady | Wykorzystuje std::atomic<bool> | Implementuje operacje lock() i unlock()|
- Philosopher - klasa reprezentująca filozofa | Cykl życia: myślenie → jedzenie | Zarządza dostępem do widelców |
- Strategia synchronizacji | Zapobieganie deadlockowi przez różną kolejność pobierania widelców | Filozofowie z parzystym ID: lewy → prawy | Filozofowie z nieparzystym ID: prawy → lewy |
## 📊 Wyniki symulacji
```bash
Starting simulation with 5 philosophers...
Philosopher 0 is thinking.
Philosopher 1 is thinking.
Philosopher 2 is eating (1 meals).
Philosopher 3 is thinking.
Philosopher 4 is eating (1 meals).
Philosopher 0 is eating (1 meals).
Philosopher 2 is thinking.
Philosopher 4 is thinking.
Philosopher 1 is eating (1 meals).
...

Simulation results:
Philosopher 0 ate 8 meals
Philosopher 1 ate 7 meals
Philosopher 2 ate 8 meals
Philosopher 3 ate 7 meals
Philosopher 4 ate 8 meals
```

| Metryka                     | Wartość                          |
|-----------------------------|----------------------------------|
| Domyślny czas symulacji     | 10 sekund                        |
| Minimalna liczba filozofów  | 2                                |
| Maksymalna liczba filozofów | ograniczona zasobami systemu     |     
| Strategia synchronizacji    | własny mutex (spinlock)          |

## Wątki i sekcje krytyczne

### Wątki w programie:
- **Wątki filozofów** (klasa `Philosopher`)
  - Każdy reprezentuje jednego filozofa przy stole
  - Cykl życia: nieskończona pętla myślenie → jedzenie
  - Zarządza własnymi widelcami (zasobami krytycznymi)

- **Wątek główny** (`main`)
  - Inicjalizuje i zarządza wątkami filozofów
  - Kontroluje czas trwania symulacji

### Sekcje krytyczne i rozwiązania:
1. **Dostęp do widelców**
   - Problem: ryzyko zakleszczenia (deadlock)
   - Rozwiązanie: asymetryczna kolejność pobierania widelców

2. **Wyświetlanie stanu**
   - Problem: wyścigi przy dostępie do cout
   - Rozwiązanie: buforowanie komunikatów w stringstream

3. **Liczenie posiłków** 
   - Problem: niespójność danych przy współbieżnej modyfikacji
   - Rozwiązanie: atomic operations na licznikach

## 📝 Podsumowanie Techniczne !
**Kluczowe elementy implementacji**
- CustomMutex: Własna implementacja mechanizmu synchronizacji
- Philosopher: Klasa encapsulująca zachowanie filozofów
- Strategia deadlock-free: Alternatywne pobieranie widelców
- Bezpieczne wyjście: Wymuszone zakończenie po czasie symulacji
 
**Statystyki**
Program zbiera i wyświetla:

- Liczbę posiłków zjedzonych przez każdego filozofa
- Czas trwania symulacji (ustalony na 10 sekund)
**Ograniczenia**
- Brak eleganckiego zakończenia wątków (wymuszone exit()
- Prosta implementacja blokady (spinlock może marnować cykle CPU)
  
  ## 📝 Autor**
  Kacper Kostrzewa
  
