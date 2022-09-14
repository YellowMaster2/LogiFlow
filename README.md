# Dokumentacja techniczna przepływu Działu Logistyki

## Przeznaczenie przepływu (po co powstał i skrótowy opis działania)
![image](https://github.com/YellowMaster2/LogiFlow/blob/main/media/1.png?raw=true)


  Celem powstania przepływu jest zautomatyzowanie procesu składania zapotrzebowania w firmie. 
  Przepływ przesyła informacje o złożonym (poprzez formularz) zapotrzebowaniu odpowiedniej osobie (przełożonemu danej osoby lub bezpośrednio Prezesowi w zależności od kwoty zapotrzebowania) i po podjęciu decyzji (akceptacji/odrzuceniu), dane zapotrzebowanie trafia do osoby z Działu Logistyki (w zależności od działu którym takowa osoba się zajmuje) w celu realizacji już zaakceptowanego zapotrzebowania lub gdy zapotrzebowanie zostanie odrzucone, trafia ono do Archiwizacji ze statusem "Odrzucone". Osoba składająca dane zapotrzebowanie jest informowana na bieżąco o statusie swojego zapotrzebowania poprzez SharePoint'ową listę "Status" oraz w każdym znaczącym momencie jest informowana poprzez mail o postępie w realizacji (potwierdzenie złożenia zapotrzebowania/zaakceptowanie zapotrzebowania/odrzucenie zapotrzebowania).
  Dodatkowo w przepływie zawarta jest przypominajka, której celem jest mailowe  przypominanie  przełożonemu o złożonych zapotrzebowaniach oczekujących na decyzję.

## Architektura systemu (z czego się składa i szczegółowy opis działania) 

  Przepływ Działu Logistyki składa się z trzech osobnych przepływów (rozdzielenie etapów przepływu w celu łatwiejszej diagnostyki w razie wystąpienia problemu po stronie programu):
   1. Składanie zapotrzebowania
      Przepływ jest uruchamiany w momencie przesłania formularza (Plumsail) dostępnego na stronie Działu Logistyki w Moje Zapotrzebowania→Złóż zapotrzebowanie. Następnie pobierane są dane użytkownika składającego zapotrzebowanie z konta Microsoft Office 365. Po potwierdzeniu, że dana osoba jest pracownikiem firmy następuje analiza produktów konkretnego zapotrzebowania i utworzenie ich na SharePoint'owej liście "Produkty Zapotrzebowania". W tym miejscu również następuje wyliczenie kosztu całkowitego zapotrzebowania. Po skompletowaniu wszystkich danych dotyczących wszystkich produktów z zapotrzebowania następuje sprawdzenie, czy koszt całkowity zapotrzebowania przekracza "maksymalny koszt dla przełożonego" - jest to zmienna, której wartość w każdej chwili można dostosować bezpośrednio przez uprawnione osoby z poziomu SharePoint'owej listy "dev_settings" i której zadanie polega na określeniu powyżej jakiej kwoty całkowitej zapotrzebowania, mail odnośnie decyzji akceptacji/odrzucenia powinien przyjść bezpośrednio do Prezesa lub do przełożonego danej osoby. W przypadku gdy dana osoba nie posiada przypisanego przełożonego za takowego uznaje się Prezesa. Następnie na SharePoint'owej liście "Składanie zapotrzebowania" tworzone jest zapotrzebowanie po utworzeniu którego wysyłany jest mail z potwierdzeniem do osoby składającej zapotrzebowanie oraz osobny do przełożonego o pojawieniu się nowego zapotrzebowania do rozpatrzenia.
   2. System powiadomień
   3. Płatności
   4. Realizacja
   5. Archiwizacja

## Bezpieczeństwo (coś o uprawnieniach)
