# Problem Ucztujących Filozofów - Implementacja w C++



## 📖 Opis problemu
Problem ucztujących filozofów to klasyczny przykład w programowaniu współbieżnym ilustrujący wyzwania synchronizacji wątków i zarządzania zasobami. Pięciu filozofów siedzi przy okrągłym stole, każdy ma przed sobą talerz, a między nimi po jednym widelcu. Filozofowie na przemian myślą i jedzą, ale aby jeść, potrzebują dwóch widelców (lewego i prawego). Problem ilustruje wyzwania deadlocku, zagłodzenia i współdzielenia zasobów.
## 🛠 Wymagania
- Kompilator C++11 (g++/clang++)
- Biblioteka pthread
- System: Windows/Linux/macOS

## 🚀 Instalacja i uruchomienie

### Kompilacja
```bash
g++ -std=c++11 -pthread philosophers.cpp -o philosophers

### uruchomienie
```bash
./philosophers [liczba_filozofów]
Przykład : ./philosophers 5

### Architektura 
Kluczowe komponenty
CustomMutex - własna implementacja mechanizmu blokady

Philosopher - klasa reprezentująca filozofa

Strategia deadlock-free - alternatywne pobieranie widelców

### Wątki i synchronizacja

Każdy filozof to osobny wątek (std::thread)

Widelce chronione przez CustomMutex

Zapobieganie deadlockowi przez różną kolejność pobierania widelców

### Wyniki Symulacji
![image](https://github.com/user-attachments/assets/b358e6b5-0d67-4e82-9f6a-a0e5d0abc524)
![image](https://github.com/user-attachments/assets/7a28c786-f470-4345-8a4b-b60a5478b34d)

Interpretacja wyników:
Każdy wątek filozofa okresowo wypisuje swój stan

Liczba w nawiasach oznacza ile posiłków zjadł dany filozof

Po zakończeniu wyświetlane jest podsumowanie zjedzonych posiłków

### Uwagi implementacyjne
Parametry symulacji:

Domyślny czas trwania: 10 sekund

Minimalna liczba filozofów: 2

Maksymalna liczba: ograniczona zasobami systemowymi

Strategia synchronizacji:

Własna implementacja mutexa (CustomMutex)

Filozofowie z parzystym ID najpierw biorą lewy widelec

Filozofowie z nieparzystym ID najpierw biorą prawy widelec

Ograniczenia:

Brak eleganckiego zakończenia wątków (wymuszone exit)

Prosta implementacja blokady (spinlock)


