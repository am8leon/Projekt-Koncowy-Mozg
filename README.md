---
# Projekt-Koncowy 🧠
---
![Obrazy Gozów Mózgu](image/zd0c.jpg)

---
# Agenda  
1. Cel stworzenia modelu
2. Zastosowane techniki
3. Dane i klasy guzów mózgu
4. Wizualizacja guzów mózgu 
5. Wyniki modelu (Optuna + CNN)
6. Kluczowe wnioski
7. Podsumowanie i rekomendacje


---
# 1. Cel stworzenia modelu
Celem projektu było opracowanie modelu głębokiego uczenia (Convolutional Neural Network, CNN), który automatycznie klasyfikuje obrazy MRI mózgu na trzy typy guzów: 
- glioma
- meningioma
- guzy przysadki

- Model ma wspomóc diagnostykę radiologiczną poprzez: przyspieszenie procesu analizy obrazów,zwiększenie dokładności klasyfikacji, dostarczenie interpretowalnych wyników (np. macierz pomyłek, F1 per klasa).
Dodatkowo, projekt pokazuje jak można wykorzystać Optunę do automatycznej optymalizacji hiperparametrów, co zwiększa wiarygodność i powtarzalność wyników.
---
# 2. Zastosowane techniki
- Convolutional Neural Network (CNN) – standard w analizie obrazów medycznych.
- Optuna – automatyczna optymalizacja hiperparametrów (learning rate, optimizer, liczba filtrów).
- Augmentacja danych – rotacje, przesunięcia, zmiany jasności → poprawa uogólniania.
- Normalizacja – stabilizuje uczenie.
- BatchNormalization – przyspiesza zbieżność i stabilizuje gradienty.
- Dropout – redukuje ryzyko przeuczenia.
- EarlyStopping + ReduceLROnPlateau – zatrzymują trening w odpowiednim momencie i dostosowują learning rate.
- MLflow – śledzenie eksperymentów i logowanie wyników.
- tf.data.Dataset – wydajne ładowanie i przetwarzanie danych.
---
# 3. Dane i klasy guzów mózgu
---
# Przykłady obrazów używanych przez model 
- Na tym zdjęciu widzimy przykładowe obrazy MRI różnych rodzajów guzów mózgu. Meningioma to guzy powierzchniowe,
  dobrze odgraniczone i przylegające do opon mózgowych. Glioma to guzy wewnętrzne, o nieregularnym kształcie,
  które trudniej odróżnić od zdrowej tkanki. Ostatni przykład pokazuje guz mózgu w ujęciu ogólnym.
  Dzięki temu zestawieniu możemy zobaczyć, jak różnią się one wyglądem i lokalizacją.

- **Wizualizacja:**

![Obrazy Gozów Mózgu](image/zd0.jpg)

---
# 4. Wizualizacja guzów mózgu 
---
- # Wizualizacja zdrowy mózg i chory mózg
- Opis zdjęcia – porównanie obrazów MRI mózgu: Na ilustracji widzimy dwa obrazy MRI mózgu zestawione obok siebie w celu porównania.
Po lewej stronie znajduje się obraz oznaczony jako „Normal” – przedstawia zdrowy mózg, w którym struktury są symetryczne i nie widać żadnych nieprawidłowości ani zmian chorobowych.
Po prawej stronie znajduje się obraz oznaczony jako „Malignant” – przedstawia mózg z widoczną zmianą nowotworową. Jasny, nieregularny obszar wskazuje na obecność guza, który zaburza prawidłową strukturę tkanki mózgowej.

- Różnice między wizualizacjami:
W obrazie normalnym tkanki są równomierne, bez wyraźnych ognisk czy asymetrii.
W obrazie złośliwym widoczny jest jasny, nieregularny obszar, który odróżnia się od reszty tkanki – to właśnie zmiana nowotworowa.
Kontrast między tymi dwoma obrazami pozwala łatwo zauważyć, jak guz wpływa na strukturę mózgu i jak bardzo różni się od obrazu zdrowego.

- **Wizualizacja:**

![Obrazy Gozów Mózgu](image/zd0b.jpg)

---
- # Wizualizacja klasyfikacja guzów mózgu
- Opis zdjęcia  widzimy przykładowe obrazy MRI trzech rodzajów guzów mózgu. Meningioma to guzy powierzchniowe,
  glioma rozwija się wewnątrz tkanki mózgowej i ma nieregularny kształt, a pituitary to guzy przysadki,
  zlokalizowane w centralnej części mózgu. To zestawienie pokazuje, jak różnią się one wyglądem i lokalizacją.
- Różnice między wizualizacjami:
  Meningioma – guzy bardziej powierzchowne, dobrze widoczne przy krawędzi mózgu.
  Glioma – guzy wewnętrzne, o nieregularnych granicach, trudniejsze do jednoznacznego odróżnienia od zdrowej tkanki.
  Pituitary – guzy zlokalizowane centralnie, w okolicy przysadki, różniące się położeniem od pozostałych typów.

- **Wizualizacja:**
![Obrazy Gozów Mózgu](image/zd0a.jpg)

---
# 4. Wyniki modelu (Optuna + CNN)
---

# Wykres dokładność modelu 
- Na tym wykresie widzimy, jak zmieniała się wartość błędu modelu w kolejnych epokach.
  Oś pozioma to epoki, a oś pionowa to strata, czyli miara błędu.
  Niebieska linia pokazuje wyniki na danych treningowych,a pomarańczowa – na danych walidacyjnych.
  Widzimy, że początkowo obie wartości spadają, ale od 4.epoki walidacja zaczyna rosnąć, co oznacza, że model zaczyna się przeuczać.

- **Wizualizacja:**

![Porównanie nowotworów](image/zd2.jpg)


---
# Wykres krzywe strat 

- Na tym wykresie widzimy, jak zmieniała się dokładność modelu w kolejnych epokach.
  Oś pozioma to epoki, a oś pionowa to dokładność, czyli procent poprawnych klasyfikacji.
  Niebieska linia pokazuje wyniki na danych treningowych, a pomarańczowa – na danych walidacyjnych. Widzimy,
  że model coraz lepiej uczy się na danych treningowych,
  ale od 3. epoki dokładność walidacyjna spada, co oznacza, że zaczyna się przeuczać.”

- **Wizualizacja:**

![Porównanie nowotworów](image/zd1.jpg)

---
# Wykres heatmap (validation)
- Na tej heatmapie widzimy macierz pomyłek, która pokazuje, jak model klasyfikuje obrazy.
  Oś pozioma to przewidywania modelu, a oś pionowa to rzeczywiste etykiety. Każdy kwadrat przedstawia liczbę przypadków – im ciemniejszy kolor, tym więcej przykładów.
  Najważniejsze są wartości na przekątnej, bo oznaczają poprawne klasyfikacje. Widzimy, że model dobrze rozpoznaje większość przypadków,
  ale zdarzają się pomyłki, szczególnie przy rozróżnianiu glioma i meningioma.

- **Wizualizacja:**

![Porównanie nowotworów](image/zd4.jpg)

---
# Heatmapa confiusion matrix  (test)
- Na tej heatmapie widzimy macierz pomyłek, która pokazuje, jak model klasyfikuje obrazy.
  Oś pozioma to przewidywania modelu, a oś pionowa to rzeczywiste etykiety. Każdy kwadrat
  przedstawia liczbę przypadków – im ciemniejszy kolor, tym więcej przykładów.
  Najważniejsze są wartości na przekątnej, bo oznaczają poprawne klasyfikacje. Widzimy,
  że model dobrze rozpoznaje większość przypadków, ale ma trudności w odróżnianiu meningioma od pozostałych klas.


- **Wizualizacja:**

![Porównanie nowotworów](image/zd5.jpg)

---
# Wykres rozkład przewidzianych klas (test)
- Na tym histogramie widzimy, jak model rozłożył swoje przewidywania pomiędzy trzy klasy guzów mózgu.
Oś pozioma przedstawia klasy, a oś pionowa liczbę próbek. Każdy słupek pokazuje, ile przypadków model przypisał do danej klasy
najwięcej do glioma, mniej do tumor, a najmniej do meningioma. Dzięki temu możemy zobaczyć,
czy model równomiernie rozpoznaje wszystkie klasy, czy też ma tendencję do częstszego wybierania jednej z nich.”

- **Wizualizacja:**

![Porównanie nowotworów](image/zd6.jpg)

---
# Histogram pewności poprawnych vs błędnych predykcji
- Na tym slajdzie widzimy dwa histogramy pokazujące, jak pewny był model przy swoich przewidywaniach.
  Oś pozioma to prawdopodobieństwo, a oś pionowa liczba przypadków. Zielony wykres pokazuje poprawne klasyfikacje
  widać, że model był wtedy zazwyczaj bardziej pewny. Czerwony wykres pokazuje błędne klasyfikacje
  tu wartości są niższe, co oznacza, że model częściej się mylił, gdy nie był do końca pewny swojego wyniku.

- **Wizualizacja:**

![Porównanie nowotworów](image/zd7.jpg)

---
# Heatmapa macierz pomyłek 
- Na tej heatmapie widzimy macierz pomyłek, która pokazuje, jak model klasyfikuje obrazy.
  Oś pozioma to przewidywania modelu, a oś pionowato rzeczywiste etykiety.
  Każdy kwadrat przedstawia liczbę przypadków – im ciemniejszy kolor, tym więcej przykładów. Najważniejsze są wartości na przekątnej,bo oznaczają poprawne klasyfikacje.
  Widzimy, że model dobrze rozpoznaje większość przypadków, ale zdarzają się pomyłki, szczególnie przy rozróżnianiu glioma i meningioma.


- **Wizualizacja:**

![Porównanie nowotworów](image/zd9ro.jpg)

---
# Wyniki modelu Grad-Cam

# Metryka klasyfikacji modelu Grad-Cam
- Na tym zdjęciu  widzimy trzy sposoby przedstawienia tego samego obrazu MRI.
Po lewej mamy oryginalny skan, w środku mapa cieplna pokazująca,które obszary były najważniejsze dla modelu, 
a po prawej nałożenie obu obrazów.Dzięki temu możemy zobaczyć, gdzie model faktycznie skupia swoją uwagę podczas klasyfikacji.

- Interpretacja wyników modelu metodą Grad-Cam:
  Lewy obraz pokazuje dane wejściowe, czyli to, co widzi lekarz.
  Środkowy obraz pokazuje dane „wewnętrzne” modelu – czyli jego uwagę i obszary, które uznał za kluczowe.
  Prawy obraz łączy oba widoki, co pozwala łatwo porównać, czy model zwraca uwagę na te same fragmenty, które byłyby istotne z punktu widzenia diagnostyki medycznej.


- **Wizualizacja:**

![Porównanie nowotworów](image/zd10.jpg)

---

# Wykres Skuteczności wykrywania typów guzów mózgu

- **Wizualizacja:**

![Porównanie nowotworów](image/zd12.jpg)


---
# Wykres Skuteczność klasyfikacji guzów mózgu

- **Wizualizacja:**

![Porównanie nowotworów](image/zd13.jpg)

---
# 5. Kluczowe wnioski
---
# Kluczowe wnioski
- Augmentacja danych znacząco poprawia skuteczność.
- BatchNormalization + Dropout → stabilność i dokładność.
- Optuna pozwoliła dobrać optymalne hiperparametry (najlepszy wynik przy learning rate ≈ 1e-3).
- F1-macro i confusion matrix pokazują, że model dobrze radzi sobie z wszystkimi klasami, choć najtrudniejsze są przypadki guzów przysadki.
- System działa stabilnie nawet przy ograniczonym zbiorze danych.

---
# 6. Podsumowanie i rekomendacje
---
# Podsumowanie i rekomendacje
- Projekt z sukcesem stworzył dokładny i dobrze uogólniający model CNN do klasyfikacji guzów mózgu na podstawie obrazów MRI. System został:
przetestowany na rzeczywistych danych (BraTS),
wsparty narzędziami śledzenia eksperymentów (MLflow),
rozszerzony o interpretowalne wyniki (confusion matrix, F1 per klasa, histogramy).
- Rekomendacje na przyszłość:
Skalowanie na większe i bardziej zróżnicowane zbiory MRI (np. 3D NIfTI).
Wykorzystanie modeli przetrenowanych (EfficientNet, ResNet).
Integracja z systemem PACS szpitalnym.
Rozszerzenie o segmentację (lokalizacja guza).
---













































  

  



