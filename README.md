# Projekt-Koncowy-Mozg

# Projekt-Koncowy-Analiza-danych
Projekt Analiza Danych mieszkania 
Analiza cen mieszkań — wynajem i zakup (2023–2024)


# Slajd 1:Projekt Koncowy Analiza danych mieszkań 
Analiza cen mieszkań — wynajem i zakup (2023–2024)

---

# Slajd 2: Agenda  
1. Cel analizy  
2. Dane i wstępne przetwarzanie  
3. Eksploracyjna analiza danych  
4. Analiza ceny za m²  
5. Kluczowe wnioski  
7. Rekomendacje  

---

# Slajd 3: Cel analizy
- Cel analizy 
Celem projektu było zbadanie rynku mieszkaniowego w Polsce na podstawie danych o wynajmie oraz zakupie mieszkań w latach 2023–2024.

---

# Slajd 4: Dane i preprocessing  
- **Źródła**:  
  - apartments_pl_2024_06.csv, apartments_pl_2023_12.csv (zakup)  
  - apartments_rent_pl_2024_06.csv (wynajem)  
- **Wczytywanie**: funkcja `read_csv_with_fallback()`  
  - Automatyczne wykrywanie kodowania (chardet)  
  - Separator `;` lub `,`  
- **Czyszczenie**:  
  - Standaryzacja nazw miast (`clean_city_column()`)

- **Wczytywanie:**
- Kod:  
  ```python
  dfs[key] = read_csv_with_fallback(path)
- **Czyszczenie miast:**
- Kod:  
  ```python
  def clean_city_column(df):
    df['city'] = df['city'].str.strip().str.title()

