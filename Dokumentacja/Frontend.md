// ================================
// form-tabs.js – obsługa zakładek
// ================================

// Event listener – odpala się, gdy cała strona (HTML) zostanie załadowana
document.addEventListener('DOMContentLoaded', function() {      // document = cały dokument HTML, addEventListener = nasłuchuje zdarzeń

    // Pobranie elementów HTML do zmiennych
    const tabs = document.querySelectorAll('.tab');             // const = stała (nie zmieniasz referencji, ale zawartość może się zmienić)
                                                               // querySelectorAll() = pobiera wszystkie elementy z klasą ".tab"
                                                               // tabs = kolekcja (NodeList) przycisków: [Logowanie, Rejestracja]

    const loginForm = document.getElementById('login-form');    // const - tworzy stałą zmienną, czyli nie można jej nadpisać
                                                               // document.getElementById() = wybiera element o konkretnym ID z HTML
                                                               // loginForm = formularz logowania

    const registerForm = document.getElementById('register-form'); // registerForm = formularz rejestracji


    // ============================
    // Funkcja przełączania formularzy
    // ============================
    function switchForm(targetForm) {                           // function = deklaracja funkcji, targetForm = argument (nazwa formularza)
        tabs.forEach(tab => tab.classList.remove('active'));    // forEach = pętla po elementach tablicy
                                                               // classList.remove('active') = usuwa klasę CSS "active" (czyli odznacza zakładkę)

        loginForm.classList.remove('active');                   // ukrywa formularz logowania
        registerForm.classList.remove('active');                // ukrywa formularz rejestracji
        
        if (targetForm === 'login') {                           // warunek: jeśli użytkownik kliknął "Logowanie"
            tabs[0].classList.add('active');                    // tabs[0] = pierwszy element w kolekcji (Logowanie)
            loginForm.classList.add('active');                  // pokazuje formularz logowania (dodaje klasę "active")
        } else if (targetForm === 'register') {                 // jeśli kliknięto "Rejestracja"
            tabs[1].classList.add('active');                    // tabs[1] = drugi element (Rejestracja)
            registerForm.classList.add('active');               // pokazuje formularz rejestracji
        }
    }
    

    // ============================
    // Obsługa kliknięć użytkownika
    // ============================
    tabs.forEach((tab, index) => {                              // forEach() = iteracja po każdym przycisku zakładki
        tab.addEventListener('click', function() {               // addEventListener() = reaguj na kliknięcie myszką
            if (index === 0) {                                   // jeśli index 0 → pierwszy tab (Logowanie)
                switchForm('login');                             // wywołaj funkcję switchForm() z argumentem 'login'
            } else {                                             // jeśli nie → drugi tab (Rejestracja)
                switchForm('register');
            }
        });

        // Obsługa klawiatury (dla dostępności)
        tab.addEventListener('keydown', function(e) {            // 'keydown' = reakcja na wciśnięcie klawisza
            if (e.key === 'Enter' || e.key === ' ') {            // e.key = klawisz, który został naciśnięty
                e.preventDefault();                              // preventDefault() = zablokuj domyślną akcję (np. scroll strony)
                this.click();                                    // this.click() = symuluj kliknięcie myszką
            }
        });
    });
    
    // Ustawienie domyślnej zakładki (logowanie)
    switchForm('login');                                         // po załadowaniu strony automatycznie pokazuje formularz logowania
});


// ============================
// Sekcja druga – efekty wizualne
// ============================

// Drugi listener – także odpala się po załadowaniu strony
document.addEventListener('DOMContentLoaded', function() {       // drugi DOMContentLoaded – nie koliduje z pierwszym
    const style = document.createElement('style');               // document.createElement() = tworzy nowy element HTML
    style.textContent = `                                        // .textContent = wpisuje tekst do elementu (tutaj kod CSS)
        .auth-form {
            opacity: 0;                                          /* przezroczystość: 0 = niewidoczny */
            transform: translateY(10px);                         /* przesunięcie w dół o 10px */
            transition: all 0.3s ease;                           /* płynne przejście animacji (0.3 sekundy) */
            pointer-events: none;                                /* blokuje interakcję z ukrytym formularzem */
        }
        
        .auth-form.active {
            opacity: 1;                                          /* pokazanie elementu */
            transform: translateY(0);                            /* przesunięcie na pierwotne miejsce */
            pointer-events: auto;                                /* ponowne włączenie interakcji */
        }
    `;
    document.head.appendChild(style);                            // appendChild() = dodaje element <style> do <head> dokumentu
});
