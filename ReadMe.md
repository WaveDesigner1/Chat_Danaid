# 🦋 Danaid – Edukacyjny model czatu z pełnym szyfrowaniem E2EE

## 🎯 Cel projektu
Danaid to **edukacyjny komunikator** stworzony w celu pokazania, jak działa szyfrowanie typu **end-to-end (E2EE)** w praktyce.  
Projekt pozwala zrozumieć:
- wymianę kluczy publicznych i prywatnych,
- szyfrowanie symetryczne i asymetryczne,
- podpisy cyfrowe oraz weryfikację tożsamości użytkowników,  
– wszystko w **czystym JavaScript, HTML i CSS**, bez frameworków.

---

## 🧠 Filozofia projektu
1. **Zero trust** – serwer nie zna żadnych danych wrażliwych.  
   Jest jedynie przekaźnikiem zaszyfrowanych treści między rozmówcami.
2. **Szyfrowanie i deszyfrowanie** odbywa się **lokalnie w przeglądarce** użytkowników.  
3. **Brak backendu** – dane są przechowywane w **plikach `.json`**, a nie w bazie SQL.  
4. **Transparentność i edukacja** – kod źródłowy jest w pełni czytelny i bogato komentowany, by pokazywać, *jak* działa każda część systemu.

---

## 💾 Struktura projektu (frontend)

| Plik | Opis |
|------|------|
| `login.html` | Strona startowa: rejestracja i logowanie użytkownika |
| `login.css` | Stylizacja ekranu logowania, animacje, motyw motyla |
| `form-tabs.js` | Logika przełączania między formularzami logowania i rejestracji |
| `chat.html` | Główne okno komunikatora (lista znajomych, rozmowy, konsola) |
| `chat.css` | Stylizacja całego interfejsu czatu |
| `butterfly.svg` | Element graficzny tła – symbol projektu Danaid 🦋 |

---

## 🔒 Bezpieczeństwo i kryptografia

Projekt zakłada pełne szyfrowanie komunikacji między użytkownikami:
- **Klucze prywatne** przechowywane są **lokalnie** (np. w przeglądarce lub jako plik).  
- **Klucze publiczne** udostępniane są w JSON-ach między użytkownikami.  
- Do szyfrowania wykorzystywane są:
  - RSA – do szyfrowania kluczy sesyjnych,
  - AES – do szyfrowania właściwych wiadomości,
  - podpis cyfrowy – dla autentyczności wiadomości.  

W dalszej fazie projektu planowana jest implementacja **protokołu X3DH + Double Ratchet** inspirowanego Signalem.

---

## 🧰 Założenia implementacyjne

- Całość oparta o **czysty JavaScript** (bez frameworków).  
- Wykorzystywane wyłącznie natywne API przeglądarki:  
  - `Web Crypto API` (szyfrowanie),  
  - `File API` (obsługa kluczy),  
  - `Fetch API` (komunikacja).  
- Dane użytkowników i wiadomości przechowywane w **plikach `.json`**.  
- Hostowanie przez **GitHub Pages** – bez kosztów, bez serwera.

---

## 💡 Cele edukacyjne

1. Zrozumienie podstaw kryptografii w kontekście komunikacji sieciowej.  
2. Nauka praktyczna **organizacji projektu frontendowego**.  
3. Poznanie **przepływu danych** między UI, logiką i strukturą danych.  
4. Praktyka w pisaniu **czystego, modularnego kodu JavaScript**.  
5. Dokumentowanie i komentowanie każdej części projektu – zrozumienie „dlaczego”, nie tylko „jak”.

---

## 📄 `form-tabs.js` — opis koncepcyjny działania

### 🎯 Cel
Ten plik odpowiada za **przełączanie między formularzem logowania i rejestracji**.  
Nie dotyka danych użytkownika – jedynie zarządza widocznością elementów interfejsu (UX).

---

### 🧩 Logika krok po kroku

1. **Po załadowaniu strony (`DOMContentLoaded`)**:
   - Skrypt pobiera elementy `.tab` (przyciski zakładek) oraz dwa formularze: `login-form` i `register-form`.

2. **Definiuje funkcję `switchForm(targetForm)`**:
   - Usuwa klasę `.active` ze wszystkich zakładek i formularzy.  
   - Aktywuje tę, którą użytkownik wybrał (login lub register).  
   - Dzięki temu użytkownik widzi tylko jeden formularz w danej chwili.

3. **Nasłuchuje kliknięć i klawiatury (Enter/Spacja)**:
   - Każdy tab może być aktywowany myszką lub klawiaturą,  
     co poprawia **dostępność (Accessibility)**.

4. **Ustawia domyślną zakładkę** – `login`.

5. **Dodaje stylizację z animacją fade-in/slide-up**:
   - Po wczytaniu strony dynamicznie wstawia CSS do `<head>`,  
     który nadaje formularzom płynne przejścia wizualne.

---

### 💬 W skrócie
> `form-tabs.js` to kontroler interfejsu – dba o wizualny i logiczny stan aplikacji.  
> Nie przetwarza danych, nie waliduje formularzy, tylko zarządza widokiem w ramach UX.

---

## 🌐 Hostowanie
Projekt zostanie opublikowany na **GitHub Pages**, co zapewni:
- darmowy publiczny dostęp,  
- prostą integrację z repozytorium,  
- brak potrzeby konfiguracji backendu.

Wersja produkcyjna będzie działać wyłącznie w przeglądarce.

---

## 📜 Autor
Projekt edukacyjny **Danaid**  
Tworzony w celach naukowych i rozwojowych — z pasją do bezpieczeństwa, kryptografii i prostoty.

