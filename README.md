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
# Wykres heatmap validacja 


- **Wizualizacja:**

![Porównanie nowotworów](image/zd6.jpg)

---
# Wykres F1 na walidacji podczas treningu
- Na wykresie przedstawiono, jak zmieniała się miara F1 (dokładniej: makro F1) modelu w trakcie procesu uczenia.
- Niebieska linia przedstawia przebieg wartości F1 w kolejnych epokach – czyli jak zmieniała się skuteczność modelu w trakcie uczenia.
- 🔵 Punkty naniesione na linię oznaczają konkretne wartości F1 w danej epoce – dzięki nim łatwo można odczytać i porównać wyniki między poszczególnymi etapami treningu.
- Opis wykresu F1 na walidacji podczas treningu: Na wykresie przedstawiono, jak zmieniała się miara F1 (dokładniej: makro F1) modelu w trakcie procesu uczenia.
- Widać lekkie wahania (np. spadek w epoce 5), ale ogólny trend jest wzrostowy, a od około 6. epoki wartości stabilizują się na wysokim poziomie.
- To sugeruje, że model osiągnął dobrą jakość i potrafi skutecznie klasyfikować dane walidacyjne.
  
- **Wizualizacja:**

![Porównanie nowotworów](image/zd3.jpg)

---

# Heatmapa Macierz pomyłek (test)
- Opis heatmapy – macierz pomyłek (Confusion Matrix): Na wykresie przedstawiono macierz pomyłek, która pokazuje, jak model klasyfikacyjny poradził sobie z rozpoznawaniem trzech klas obrazów mózgu.
- Kolory kwadratów odzwierciedlają liczebność przypadków – im ciemniejszy kolor, tym więcej przykładów znajduje się w danej komórce.
- Wartości liczbowe w każdym kwadracie pokazują dokładną liczbę przypadków, np. ile obrazów z klasy brain_glioma zostało poprawnie rozpoznanych jako brain_glioma, a ile błędnie zaklasyfikowanych do innych klas.

- **Wizualizacja:**

![Porównanie nowotworów](image/zd5.jpg)

---
# 6.Wyniki modelu na dodatkowym zbiorze danych metryka optuna
-  Na Heatmapie  przedstawiono macierz pomyłek, która pokazuje, jak model klasyfikacyjny radzi sobie z rozpoznawaniem trzech klas obrazów mózgu: brain_glioma, brain_menin oraz brain_tumor.
- Kolory kwadratów odzwierciedlają liczebność przypadków – im ciemniejszy kolor, tym więcej przykładów znajduje się w danej komórce. 
- Wartości liczbowe w każdym kwadracie pokazują dokładną liczbę przypadków, np. ile obrazów z klasy brain_glioma zostało poprawnie rozpoznanych jako brain_glioma, a ile błędnie zaklasyfikowanych do innych klas.


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













































  

  



