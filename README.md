# Dokumentacja techniczna przepływu Działu Logistyki

## Przeznaczenie przepływu (po co powstał i skrótowy opis działania)
![image](https://github.com/YellowMaster2/LogiFlow/blob/main/media/Z%C5%82%C3%B3%C5%BC%20zapotrzebowanie.gif?raw=true)


  Celem powstania przepływu jest zautomatyzowanie procesu składania zapotrzebowania w firmie. 
  Przepływ przesyła informacje o złożonym (poprzez formularz) zapotrzebowaniu odpowiedniej osobie (przełożonemu danej osoby lub bezpośrednio Prezesowi w zależności od kwoty zapotrzebowania) i po podjęciu decyzji (akceptacji/odrzuceniu), dane zapotrzebowanie trafia do osoby z Działu Logistyki (w zależności od działu którym takowa osoba się zajmuje) w celu realizacji już zaakceptowanego zapotrzebowania lub gdy zapotrzebowanie zostanie odrzucone, trafia ono do Archiwizacji ze statusem "Odrzucone". Osoba składająca dane zapotrzebowanie jest informowana na bieżąco o statusie swojego zapotrzebowania poprzez SharePoint'ową listę "Status" oraz w każdym znaczącym momencie jest informowana poprzez mail o postępie w realizacji (potwierdzenie złożenia zapotrzebowania/zaakceptowanie zapotrzebowania/odrzucenie zapotrzebowania).
  Dodatkowo w przepływie zawarta jest przypominajka, której celem jest mailowe  przypominanie  przełożonemu o złożonych zapotrzebowaniach oczekujących na decyzję.

  [Diagram ukazujący schemat działania flow](https://evatronix-my.sharepoint.com/:u:/p/slawomir_zyla/EdyBaoCOFFJCrlYMgJ33yJgBpljSFizM_o_xBd4VC2TB4A?e=gSnKod)

## Architektura systemu (z czego się składa i szczegółowy opis działania) 

  Przepływ Działu Logistyki składa się z kilku osobnych przepływów (rozdzielenie etapów przepływu w celu łatwiejszej diagnostyki w razie wystąpienia problemu po stronie programu):
   1. Składanie zapotrzebowania

      Przepływ jest uruchamiany w momencie przesłania formularza (Plumsail) dostępnego na stronie Działu Logistyki w Moje Zapotrzebowania→Złóż zapotrzebowanie.
      ![image](https://github.com/YellowMaster2/LogiFlow/blob/main/media/2.png?raw=true)


       Następnie pobierane są dane użytkownika składającego zapotrzebowanie z konta Microsoft Office 365. Po potwierdzeniu, że dana osoba jest pracownikiem firmy następuje analiza produktów konkretnego zapotrzebowania i utworzenie ich na SharePoint'owej liście "Produkty Zapotrzebowania". W tym miejscu również następuje wyliczenie kosztu całkowitego zapotrzebowania. Po skompletowaniu wszystkich danych dotyczących wszystkich produktów z zapotrzebowania następuje sprawdzenie, czy koszt całkowity zapotrzebowania przekracza "maksymalny koszt dla przełożonego" - jest to zmienna, której wartość w każdej chwili można dostosować bezpośrednio przez uprawnione osoby z poziomu SharePoint'owej listy "dev_settings" i której zadanie polega na określeniu powyżej jakiej kwoty całkowitej zapotrzebowania, mail odnośnie decyzji akceptacji/odrzucenia powinien przyjść bezpośrednio do Prezesa lub do przełożonego danej osoby. W przypadku gdy dana osoba nie posiada przypisanego przełożonego za takowego uznaje się Prezesa. Następnie na SharePoint'owej liście "Składanie zapotrzebowania" tworzone jest zapotrzebowanie po utworzeniu którego wysyłany jest mail z potwierdzeniem do osoby składającej zapotrzebowanie oraz osobny do przełożonego o pojawieniu się nowego zapotrzebowania do rozpatrzenia. Równocześnie tworzony jest status umożliwiający podgląd obecnego stanu zapotrzebowania wyświetlany indywidualnie dla każdej osoby składającej w jej panelu Moje zapotrzebowania

   2. System powiadomień
   3. System statusów
    
      Przepływ uruchamiany jest w momencie modyfikacji zapotrzebowania na liście "Realizacja". Lista "Realizacja" wyświetlana jest tylko dla osób z działu Logistyki i wyświetlane są w niej zapotrzebowania uprzednio zaakceptowane, przypisane do osoby, która konkretnym działem się zajmuje. Przepływ sprawdza stan trzech kolumn listy "Realizacja": Zamówione, Dostarczone, Opłacone i w zależności od ich stanu zmieniany jest status na panelu "Moje zapotrzebowania". W sytuacji gdy zapotrzebowanie jest Zamówione status zmienia się na "Zamówione", gdy zapotrzebowanie jest Zamówione i Dostarczone status zmienia się na "Dostarczone", a gdy zapotrzebowanie jest Zamówione, Dostarczone i Opłacone wtedy status zmienia się na "Zrealizowane" i zapotrzebowanie trafia do Archiwizacji, aby Zrealizowane zapotrzebowania nie "zaśmiecały" listy osobom z działu Logistyki.  
   
   4. Realizacja

      Przepływ uruchamiany jest w momencie modyfikacji zapotrzebowania na SharePoint'owej liście "Składanie zapotrzebowania". Pobierane są wszystkie informacje dotyczące konkretnego zapotrzebowania o przypisanym mu identyfikatorze. Na liście "dev_settings" do każdego działu firmy przypisana jest odpowiednia osoba, która się nim zajmuje. W przepływie sprawdzana jest dana modyfikacja: czy jest to Akceptacja czy też Odrzucenie. W przypadku akceptacji pobierana jest informacja o dziale, z którego pracownik złożył zapotrzebowanie i w zależności od przypisanej do niego osobie z Działu Logistyki, takowej osobie wysyłany jest mail z informacją o już zaakceptowanym zapotrzebowaniu oczekującym na realizacje. Dodatkowo po akceptacji zapotrzebowania i utworzeniu go na liście "Realizacja" zmienia się status zapotrzebowania z "Oczekuje na zatwierdzenie" na "Oczekuje na realizacje" w panelu "Moje zapotrzebowania". W przypadku odrzucenia zapotrzebowanie trafia na liste "Odrzucone" ze statusem "Odrzucone" (Archiwizacja). 
      
   5. Archiwizacja
   todo Archiwizacja

## Bezpieczeństwo (coś o uprawnieniach)
todo Uprawnienia
## Instrukcja obsługi
##### 1. Składanie zapotrzebowania
1. W celu złożenia zapotrzebowania należy wejść na stronę główną [Działu logistyki](https://evatronix.sharepoint.com/sites/Logistyka "Przejdź na stronę Działu logistyki"), a następnie wejść w "Moje zapotrzebowania".

![image](https://github.com/YellowMaster2/LogiFlow/blob/main/media/3.png?raw=true)

2. Następnie należy nacisnąć przycisk "Złóż zapotrzebowanie".

![image](https://github.com/YellowMaster2/LogiFlow/blob/main/media/4.png?raw=true)

3. Po przekierowaniu na stronę internetową formularza, należy zalogować się na służbowe konto Office 365.

![image](https://github.com/YellowMaster2/LogiFlow/blob/main/media/5.png?raw=true)

4. Po zalogowaniu się na konto należy podążać za instrukcjami zawartymi w formularzu.
5. Po wypełnieniu i wysłaniu formularza, na skrzynkę pocztową trafi e-mail z potwierdzeniem złożenia zapotrzebowania.

##### 2. Akceptacja zapotrzebowania (przełożony)
1. Aby zaakceptować złożone zapotrzebowanie należy wejść na listę "Składanie zapotrzebowania" na której wyświetlane są zapotrzebowania wymagające uwagi przełożonego.
<image>
2. Na liście wystarczy kliknąć na kolumne "Akceptacja" przy konkretnym zaapotrzebowaniu następnie przejść wiersz niżej aby stan mógł się zapisać. Po udanej akceptacji cały wiersz podświetla się na kolor zielony.
<image>
3. Po akceptacji do osoby składającej zapotrzebowanie przychodzi mail z informacją o pozytywnym rozpatrzeniu owego zapotrzebowania.

##### 3. Realizacja zapotrzebowania (dział Logistyki)
1. Po zaakceptowaniu zapotrzebowania tworzone jest ono na liście "Realizacja", gdzie wyświetlane są one osobom z działu Logistyki w zależności od tego jakim działem się zajmują.
<image>
2. Osoba z działu Logistyki ma do odznaczenia trzy etapy w zaakceptowanym zapotrzebowaniu: Zamówione, Dostarczone, Opłacone. Gdy zapotrzebowanie zostanie tylko Zamówione zaznacza kolumne Zamówione (zaznaczenie wiersza na kolor czerwony).
<image>
3. Gdy zapotrzebowanie zostanie Zamówione oraz Opłacone zaznaczamy kolumny Zamówione i Opłacone (zaznaczenie na kolor pomarańczowy).
<image>
4. Gdy zapotrzebowanie zostanie Zamówione, Opłacone i Dostarczone zaznaczamy kolumny Zamówione, Opłacone i Dostarczone (zaznaczenie na kolor zielony).
<image>

##### 4. Statusy
1. Dostępne są poprzez wejście na stronie głównej działu Logistyki, a następnie klikając w "Moje zapotrzebowania".
<image>
2. Gdy zapotrzebowanie jest Zamówione status przy zapotrzebowaniu jest wyświetlany jako "Zamówione".
<image>
3. Gdy zapotrzebowanie jest Zamówione oraz Dostarczone status przy zapotrzebowaniu jest wyświetlany jako "Dostarczone".
<image>
4. Gdy zapotrzebowanie jest Zamówione, Dostarczone oraz Opłacone status przy zapotrzebowaniu jest wyświetlany jako "Zrealizowane".
<image>
5. Składający zapotrzebowanie informowany jest drogą mailową o każdej zmianie statusu jego złożonego zapotrzebowania.

##### 5. Kontrola płatności
![image](https://media.giphy.com/media/TYlus7VAr9c4M/giphy.gif)
