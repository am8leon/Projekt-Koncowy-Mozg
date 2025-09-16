# Projekt-Koncowy 🧠
Automatyczna klasyfikacja guzów mózgu na podstawie obrazów MRI 
z wykorzystaniem konwolucyjnych sieci neuronowych
---

# Agenda  
1. Cel stworzenia modelu
2. Zastosowane techniki 
4. Wyniki modelu opartego o metrykę Optuna
5. Wyniki modelu na dodatkowym zbiorze danych metryka optuna
6. Wizualizacje
7. Kluczowe wnioski
8. Podsumowanie i Rekomendacje  

---
# 1. Cel stworzenia modelu
Celem projektu było opracowanie modelu głębokiego uczenia (CNN), który automatycznie klasyfikuje obrazy MRI mózgu na trzy typy guzów: glioma, meningioma i guzy przysadki.
Model ma wspomóc diagnostykę radiologiczną poprzez przyspieszenie i zwiększenie dokładności wykrywania oraz klasyfikacji nowotworów.
---
# 2. Zastosowane techniki
- Convolutional Neural Network to sprawdzony standard w zadaniach analizy obrazów medycznych.
- Augmentacja i normalizacja poprawiają uogólnianie i stabilność uczenia.
- BatchNormalization i Adam przyspieszają zbieżność.
- Dropout to mocna regularyzacja przy ograniczonym zestawie obrazów.
- Porównanie wariantów pozwala dobrać najlepszą kombinację hiperparametrów i architektury.

---
# Przykłady obrazów używanych przez model 
- Takie przykłady służą do zobrazowania różnicy między zdrowymi i chorymi skanami w zadaniu automatycznej klasyfikacji czy wspomagania diagnostyki.
- Klasy gózów mózgu
- brain_glioma – Zawiera obrazy guzów glejowych, które powstają z komórek glejowych w mózgu. Mogą mieć różny stopień złośliwości.
- brain_menin – Zawiera obrazy meningiomów, czyli nowotworów wywodzących się z opon mózgowych. Często są łagodne, ale ich położenie może powodować poważne komplikacje.
- brain_tumor – Prawdopodobnie folder zawiera mieszane przypadki różnych nowotworów mózgu, bez podziału na konkretny typ.

- **Wizualizacja:**

![Obrazy Gozów Mózgu](image/zd0.jpg)

---
#  Wyniki modelu opartego o metrykę Optuna
---

# Wykres dokładność modelu 




- **Wizualizacja:**

![Porównanie nowotworów](image/zd2.jpg)


---
# Wykres krzywe strat 

- Na wykresie przedstawiono przebieg straty (loss) modelu uczenia maszynowego w trakcie treningu.
- Obie krzywe mają tendencję spadkową, co oznacza, że model uczy się i poprawia swoje wyniki w kolejnych epokach.
- 🔵 Niebieska linia pokazuje stratę na zbiorze treningowym (Train loss) – czyli jak dobrze model uczy się na danych, które zna.
- 🟠 Pomarańczowa linia pokazuje stratę na zbiorze walidacyjnym (Val loss) – czyli jak dobrze model radzi sobie na nowych danych, których wcześniej nie widział.

- **Wizualizacja:**

![Porównanie nowotworów](image/zd1.jpg)


---
# Wykres F1 na walidacji podczas treningu
- Na wykresie przedstawiono, jak zmieniała się miara F1 (dokładniej: makro F1) modelu w trakcie procesu uczenia.
- 🔵 Niebieska linia przedstawia przebieg wartości F1 w kolejnych epokach – czyli jak zmieniała się skuteczność modelu w trakcie uczenia.
- ⚪ Punkty naniesione na linię oznaczają konkretne wartości F1 w danej epoce – dzięki nim łatwo można odczytać i porównać wyniki między poszczególnymi etapami treningu.
- Opis wykresu F1 na walidacji podczas treningu: Na wykresie przedstawiono, jak zmieniała się miara F1 (dokładniej: makro F1) modelu w trakcie procesu uczenia.
- Widać lekkie wahania (np. spadek w epoce 5), ale ogólny trend jest wzrostowy, a od około 6. epoki wartości stabilizują się na wysokim poziomie.
- To sugeruje, że model osiągnął dobrą jakość i potrafi skutecznie klasyfikować dane walidacyjne.
  
- **Wizualizacja:**

![Porównanie nowotworów](image/zd3.jpg)

---
# Wykres F1 dla poszczególnych klas test
- Opis histogramu F1 dla poszczególnych klas (TEST): Na wykresie przedstawiono wyniki modelu w postaci miary F1 dla trzech różnych klas diagnozowanych na obrazach mózgu.
- Im wyższa wartość, tym lepiej model radzi sobie z poprawnym rozpoznawaniem danej klasy.
- Słupki pokazują wartości F1 uzyskane przez model dla każdej z klas.
- W tym przypadku wszystkie słupki sięgają wysoko, co oznacza, że model osiągnął bardzo dobre wyniki w rozpoznawaniu każdej z trzech klas.

- **Wizualizacja:**

![Porównanie nowotworów](image/zd4.jpg)

---
# Heatmapa Macierz pomyłek (test)
- Ta heatmapa to macierz pomyłek  która pokazuje, jak dobrze model klasyfikacyjny rozpoznaje trzy rodzaje zmian w mózgu: glioma, meningioma i inne guzy mózgu. Jest to narzędzie do oceny jakości działania modelu — pozwala zobaczyć, ile przypadków zostało sklasyfikowanych poprawnie, a ile błędnie.

- Znaczenie poszczególnych kwadratów
Każdy kwadrat pokazuje liczbę przypadków, które należały do danej klasy rzeczywistej (oś pionowa) i zostały zaklasyfikowane jako dana klasa przewidziana (oś pozioma).
Kwadraty na przekątnej (od lewego górnego rogu do prawego dolnego) to poprawne klasyfikacje — im większe liczby w tych polach, tym lepiej działa model.
Kwadraty poza przekątną to pomyłki modelu — pokazują, ile przypadków zostało źle zaklasyfikowanych i na co zostały „zamienione”.

- Znaczenie kolorów
Kolor jest tym ciemniejszy, im większa liczba przypadków w danym kwadracie.
Najciemniejsze pola oznaczają najczęściej występujące kombinacje rzeczywistej i przewidzianej klasy.
Jaśniejsze pola oznaczają rzadsze przypadki.

- Rodzaj danych w kwadratach
W każdym polu znajduje się liczba całkowita – to liczba próbek (np. obrazów MRI), które wpadły do tej konkretnej kategorii rzeczywista–przewidziana.
Dane te są wynikiem testu modelu na zestawie danych, którego model wcześniej nie widział.

- **Wizualizacja:**

![Porównanie nowotworów](image/zd5.jpg)

---
#  Przykłady  klasyfikacji mózgu
- Tutaj mamy przykłady obrazów MRI mózgu wraz z opisem prawidłowej diagnozy i diagnozy przewidzianej przez model. 
Dzięki temu możemy wizualnie ocenić, w których przypadkach model działa poprawnie, a w których się myli.
To pozwala lepiej zrozumieć, jakie typy zmian w mózgu są dla modelu łatwe do rozpoznania, a które sprawiają mu trudność.


- **Wizualizacja:**

![Porównanie nowotworów](image/zd8.jpg)

---
# 6.Wyniki modelu na dodatkowym zbiorze danych metryka optuna

- **Wizualizacja:**

![Porównanie nowotworów](image/zd9ro.jpg)

---
# Kluczowe wnioski
Augmentacja danych znacząco poprawia skuteczność modeli.
Batch Normalization + Dropout wspierają stabilność i dokładność.
Największą skuteczność osiągnięto na modelach z rozszerzeniami, przy learning rate = 1e-3.
Grad-CAM potwierdza, że model uczy się na właściwych strukturach anatomicznych.
System działa dobrze przy małych rozmiarach danych i może być łatwo wdrożony.

---
# Podsumowanie i rekomendacje
Projekt z sukcesem stworzył dokładny i dobrze uogólniający model CNN do klasyfikacji guzów mózgu na podstawie obrazów MRI. System został:
Przetestowany na rzeczywistych danych (BraTS),
Wsparty narzędziami śledzenia eksperymentów (MLflow),
Rozszerzony o interpretowalne wyniki (Grad-CAM, ROC, confusion matrix).
- Rekomendacje na przyszłość:
Skalowanie na większe i bardziej zróżnicowane zbiory MRI (np. 3D NIfTI).
Wykorzystanie modeli przetrenowanych (np. EfficientNet, ResNet).
Integracja z systemem PACS szpitalnym.
Automatyczna lokalizacja guza (segmentacja) jako uzupełnienie klasyfikacji.

---













































  

  



