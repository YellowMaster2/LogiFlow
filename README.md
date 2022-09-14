# Dokumentacja techniczna przepływu Działu Logistyki

## Przeznaczenie przepływu (po co powstał i skrótowy opis działania)
[image](https://user-images.githubusercontent.com/53380858/190110336-dde8b190-9fd2-4013-86c6-e63b0ffd9bab.png)


  Celem powstania przepływu jest zautomatyzowanie procesu składania zapotrzebowania w firmie. Przepływ przesyła informacje o złożonym (poprzez formularz) zapotrzebowaniu odpowiedniej osobie (przełożonemu danej osoby lub bezpośrednio Prezesowi w zależności od kwoty zapotrzebowania) i po podjęciu decyzji (akceptacji/odrzuceniu), dane zapotrzebowanie trafia do osoby z Działu Logistyki (w zależności od działu którym takowa osoba się zajmuje) w celu realizacji już zaakceptowanego zapotrzebowania lub gdy zapotrzebowanie zostanie odrzucone, trafia ono do Archiwizacji ze statusem "Odrzucone". Osoba składająca dane zapotrzebowanie jest informowana na bieżąco o statusie swojego zapotrzebowania poprzez SharePoint'ową listę "Status" oraz w każdym znaczącym momencie jest informowana poprzez mail o postępie w realizacji (potwierdzenie złożenia zapotrzebowania/zaakceptowanie zapotrzebowania/odrzucenie zapotrzebowania). Dodatkowo w przepływie zawarta jest przypominajka, której celem jest mailowe  przypominanie  przełożonemu o złożonych zapotrzebowaniach oczekujących na decyzję.

## Architektura systemu (z czego się składa i szczegółowy opis działania) 

  Przepływ Działu Logistyki składa się z trzech osobnych przepływów (rozdzielenie etapów przepływu w celu łatwiejszej diagnostyki w razie wystąpienia problemu po stronie programu):
   1. Składanie zapotrzebowania
      Przepływ uruchamiany w momencie przesłania formularza (Plumsail) dostępnego na stronie Działu Logistyki
   2. System powiadomień
   3. Płatności
   4. Realizacja

## Bezpieczeństwo (coś o uprawnieniach)