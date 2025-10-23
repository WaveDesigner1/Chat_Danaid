🧩 ALGORYTM REJESTRACJI — KONCEPCJA
1️⃣ Użytkownik inicjuje rejestrację (frontend)

Użytkownik wprowadza nazwę (username).

Przeglądarka generuje parę kluczy kryptograficznych (publiczny / prywatny).

Klucz prywatny zostaje zapisany lokalnie (nigdy nie wychodzi z urządzenia).

Klucz publiczny wraz z nazwą użytkownika są wysyłane do backendu.

2️⃣ Backend weryfikuje dane

Sprawdza, czy nazwa użytkownika już istnieje w katalogu (users).

Jeśli tak → odrzuca rejestrację.

Jeśli nie → przechodzi do tworzenia struktur danych użytkownika.

3️⃣ Backend tworzy infrastrukturę użytkownika

Tworzy w JSONBin:

inbox bin (pusta skrzynka odbiorcza),

account bin (profil użytkownika zawierający publiczne dane).

Zapisuje identyfikatory i klucze do tych binów (accountId, inboxId itd.).

4️⃣ Backend aktualizuje katalog użytkowników

Dodaje nowego użytkownika do lokalnego katalogu (users), zawierającego:

nazwę użytkownika,

publiczny klucz,

referencję do jego konta i inboxa.

Zapisuje katalog w pamięci lub w kopii zapasowej (users.json).

5️⃣ Backend zwraca dane do frontendu

Wysyła użytkownikowi dane niezbędne do dalszego działania:

identyfikatory jego binów,

klucze dostępu (tylko te należące do niego).

6️⃣ Frontend finalizuje rejestrację

Zapisuje w pamięci lokalnej:

dane konta i klucze dostępowe,

prywatny klucz użytkownika.

Rejestracja zostaje zakończona — użytkownik posiada pełną parę kluczy i swoje biny.

🔁 DATA FLOW (opis przepływu danych)
[Frontend: Przeglądarka]
    ↓  (1) wysyła { username, publicKey }
[Backend: Node.js API]
    ↓  (2) sprawdza unikalność w katalogu users
    ↓  (3) tworzy inbox i account bin w JSONBin
    ↓  (4) aktualizuje katalog użytkowników (in-memory + kopia users.json)
    ↓  (5) zwraca identyfikatory i klucze dostępu
[Frontend]
    ↓  (6) zapisuje dane lokalnie i kończy proces

🔒 ZASADY BEZPIECZEŃSTWA

Klucz prywatny nigdy nie trafia do backendu ani JSONBin.

Katalog users zawiera tylko publiczne dane (username, publicKey, identyfikatory).

Backend jako jedyny ma prawo modyfikować katalog użytkowników.

JSONBin służy wyłącznie do przechowywania indywidualnych danych użytkowników, a nie do globalnych list.
