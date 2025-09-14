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
# Wykres krzywe strat 
- Ten wykres pokazuje, jak zmieniała się wartość straty (loss) w trakcie uczenia modelu. Strata to miara błędu — im mniejsza, tym lepiej model dopasowuje się do danych. Wykres przedstawia zarówno wyniki na danych treningowych, jak i na danych walidacyjnych, dzięki czemu możemy ocenić, czy model uczy się w sposób prawidłowy i czy potrafi generalizować do nowych danych.

- Znaczenie linii
Niebieska linia – „Strata trening”: pokazuje, jak zmieniała się strata na danych, na których model był trenowany. Widać wyraźny trend spadkowy, co oznacza, że model coraz lepiej dopasowuje się do danych treningowych.

- Pomarańczowa linia – „Strata walidacja”: przedstawia stratę na danych walidacyjnych, czyli takich, których model nie widział podczas uczenia. Jej przebieg jest bardziej falujący, ale również ogólnie maleje, co sugeruje, że model poprawia swoje wyniki także na nowych danych.

- Na tym wykresie widzimy, jak zmieniała się wartość błędu modelu w trakcie treningu. Oś pozioma to kolejne epoki, a oś pionowa to wartość straty. Niebieska linia pokazuje błąd na danych treningowych, a pomarańczowa – na danych walidacyjnych. Obie linie ogólnie opadają, co oznacza, że model uczy się coraz lepiej, choć w przypadku walidacji widać większe wahania.”

- **Wizualizacja:**

![Porównanie nowotworów](image/zd1.jpg)

---
# Wykres dokładność modelu 


- **Wizualizacja:**

![Porównanie nowotworów](image/zd2.jpg)

---
# Wykres F1 na walidacji podczas treningu
- Wykres liniowy pokazuje, jak zmieniała się skuteczność modelu w trakcie jego uczenia. Mierzymy ją za pomocą wskaźnika Macro F1 na zbiorze walidacyjnym, czyli na danych, których model nie widział podczas treningu, ale które służą do sprawdzania, czy model faktycznie się poprawia.
- Znaczenie linii na wykresie
Linia pokazuje, jak zmieniała się wartość Macro F1 w kolejnych epokach.
Widać ogólny trend wzrostowy — model uczy się coraz lepiej, choć w połowie treningu (około 5. epoki) następuje chwilowy spadek, a następnie ponowny wzrost i osiągnięcie najwyższych wartości w końcowych epokach.
Taki przebieg jest normalny — chwilowe spadki mogą wynikać z tego, że model „szuka” najlepszego sposobu dopasowania się do danych.

- Na tym wykresie widzimy, jak zmieniała się skuteczność naszego modelu w trakcie treningu. 
Oś pozioma to kolejne epoki, czyli etapy uczenia, a oś pionowa to wynik Macro F1 na danych walidacyjnych. 
Linia pokazuje, że z czasem model poprawiał swoje wyniki, z drobnym spadkiem w połowie, po czym osiągnął najwyższą skuteczność pod koniec treningu.

- **Wizualizacja:**

![Porównanie nowotworów](image/zd3.jpg)

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
# Wykres F1 dla posczególnych klas test

- Ten wykres słupkowy pokazuje, jak dobrze model klasyfikacyjny rozpoznaje poszczególne typy zmian w mózgu. 
Miarą skuteczności jest tutaj F1 score — wskaźnik, który łączy w sobie precyzję i czułość modelu. Wartość F1 mieści się w przedziale od 0 do 1, gdzie 1 oznacza perfekcyjną skuteczność.

- Znaczenie słupków
Każdy słupek odpowiada jednej klasie i pokazuje, jak dobrze model radzi sobie z jej rozpoznawaniem.
Wysokość słupka to wartość F1 — im wyższy słupek, tym lepsza skuteczność modelu dla danej klasy.
W tym przypadku wszystkie słupki są bardzo wysokie, bliskie wartości 1, co oznacza, że model osiąga bardzo wysoką skuteczność w rozpoznawaniu wszystkich trzech typów zmian.

- Na tym wykresie widzimy skuteczność modelu dla każdej z trzech klas. Oś pozioma to nazwy klas, a oś pionowa to wartość wskaźnika F1. Wysokie słupki, bliskie wartości 1, 
oznaczają, że model bardzo dobrze rozpoznaje wszystkie typy zmian w mózgu, praktycznie bez większych pomyłek.”

- **Wizualizacja:**

![Porównanie nowotworów](image/zd4.jpg)

---
#  Przykłady  klasyfikacji mózgu
- Tutaj mamy przykłady obrazów MRI mózgu wraz z opisem prawidłowej diagnozy i diagnozy przewidzianej przez model. 
Dzięki temu możemy wizualnie ocenić, w których przypadkach model działa poprawnie, a w których się myli.
To pozwala lepiej zrozumieć, jakie typy zmian w mózgu są dla modelu łatwe do rozpoznania, a które sprawiają mu trudność.


- **Wizualizacja:**

![Porównanie nowotworów](image/zd6o.jpg)

---
# 6.Wyniki modelu na dodatkowym zbiorze danych metryka optuna

- **Wizualizacja:**

![Porównanie nowotworów](image/zd1or.jpg)

---
# . Wizualizacje
W projekcie zaimplementowano liczne wizualizacje:
Krzywe dokładności (accuracy, val_accuracy) dla każdego eksperymentu.
Macierz pomyłek (confusion matrix) dla najlepszego modelu.
Grad-CAM – interpretacja obszarów obrazu decydujących o klasyfikacji.
ROC Curve + AUC dla każdej klasy.
Histogramy: skuteczności, błędnych predykcji, rozkładu klas.

---
# . Kluczowe wnioski
Augmentacja danych znacząco poprawia skuteczność modeli.
Batch Normalization + Dropout wspierają stabilność i dokładność.
Największą skuteczność osiągnięto na modelach z rozszerzeniami, przy learning rate = 1e-3.
Grad-CAM potwierdza, że model uczy się na właściwych strukturach anatomicznych.
System działa dobrze przy małych rozmiarach danych i może być łatwo wdrożony.

---
# . Podsumowanie i rekomendacje
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













































  

  



