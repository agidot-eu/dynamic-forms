# dynamic-forms (Opis formatu GUI - Structura DynamicForms DSL)
Prosty opis formularzy - zoptymalizowany do pracy z AI - podeślij link do tej strony do chatGPT i poproś o wygenerowanie widoku 

## Szablon startowy

```
:PozyczkaOnline form
Szablon nagłówka 3 h3
nazwa sekcji section
 Nagłówek 5 h5
 Nip textbox
 NumerTelefonu textbox
 AdresEmail textbox
Druga sekcja section
 Szablon nagłówka 5 h5


Header header - przykładowy layout aplikacji
 LogoFirmy img datasource="https://structura.agidot.eu/api/upload-image/get/image-13.png"
 g1
 Rejestracja link 
 DaneFinansowe link
 Realizacja link
Sidebar sidebar
 column
  LogoFirmy img datasource="https://structura.agidot.eu/api/upload-image/get/image-13.png"
  NazwaFirmy label
  g2
 panelmenu
  Analiza panelmenuitem
  Klienci panelmenuitem
 column
  g3 
  www.agidot.eu label
  Copyright Ⓒ 2025 label


```

## Generator widoku online

Narzędzie online generujące gui na podstawie opisu
1. Otwórz formularz
![image](https://github.com/user-attachments/assets/e8f424ce-1022-4bbf-8df5-b32b76a12c83)
2. Wprowadzć opis widoku do pola tekstowego
   ![image](https://github.com/user-attachments/assets/049dd243-c602-45b0-a994-25ed4fd07e0f)
3. Kliknij generuj - poniżej pojawi się log z parsowania formatki
4. Kliknij 'Przejdź do /df/{id}' - pojawi się formatka
![image](https://github.com/user-attachments/assets/038b3b9f-4ed2-4ba6-bb4d-2e1a85e015a3)


## Współpraca z AI - chatGPT

![image](https://github.com/user-attachments/assets/602ce7e3-1d31-49e8-a3c1-e22b232c13f1)

Przykłądowy prompt
```
bazując na https://agidot.eu/blog/dynamic-forms-ver-9/
wygeneruj mi tekstowy opis formatki:

formatka rejestrująca nowy typ produktu z jego nazwą, kodem, typem, jednostką miary, wagą jednostkową oraz wagą opakowania i ilością w opakowaniu
```

Odpowiedź chata
![image](https://github.com/user-attachments/assets/92f53ae5-826b-4677-b7ee-6aecd292ad6e)

```
:NowyProdukt form
Rejestracja nowego typu produktu h3

DanePodstawowe section
 Dane podstawowe produktu h5
 Nazwa textbox - Nazwa produktu
 Kod textbox - Kod produktu
 Typ dropdown datasource="['Elektronika','Odzież','Spożywcze','Inne']" - Wybierz typ produktu
 JednostkaMiary dropdown datasource="['szt.','kg','l','m']" - Jednostka miary

ParametryLogistyczne section
 Parametry logistyczne h5
 WagaJednostkowa textbox - Waga jednostkowa (kg)
 WagaOpakowania textbox - Waga opakowania zbiorczego (kg)
 IloscWOpakowaniu textbox - Ilość sztuk w opakowaniu

```
![image](https://github.com/user-attachments/assets/2ac1e7f0-44ec-4c33-a9c2-1982bfb8f29d)



## 🔷 Struktura ogólna

Format opisuje interfejs użytkownika w postaci tekstowej. Wcięcia oznaczają strukturę zagnieżdżeń. Każdy element odpowiada komponentowi UI.

---

## ✅ Formularz (`form`)
- Definicja: `:NazwaFormularza form`
- Odpowiada klasie `FormDefinition`
- Zawiera listę kontrolek

### Przykład:
```
:DanePodstawowe form
Imie textbox - Imię użytkownika
AkceptujeRegulamin checkbox
ListaFirm dropdown datasource="['firma1','firma2']"
```

---

## ✅ Kontrolki treści (`ContentControl`)

| DSL            | Klasa C#        | Opis                                           |
|----------------|-----------------|------------------------------------------------|
| `textbox`      | `TextBox`       | Pole tekstowe                                 |
| `checkbox`     | `CheckBox`      | Pole wyboru                                   |
| `dropdown`     | `ComboBox`      | Lista rozwijana (z `datasource`)              |
| `img`          | `Image`         | Obrazek (z `datasource` URL)                  |
| `label`        | `TextBlock`     | Etykieta                                       |
| `link`         | `Link`          | Link (z `datasource`)                         |
| `h1`–`h6`      | `Heading`       | Nagłówek (poziom `HeaderLevel`)               |

---

## ✅ Kontrolki kontenerowe (`ContainerControl`)

| DSL            | Klasa C#        | Opis                                           |
|----------------|-----------------|------------------------------------------------|
| `section`      | `Section`       | Sekcja formularza                             |
| `tabs`         | `Tabs`          | Zakładki                                       |
| `tab`          | `Tab`           | Pojedyncza zakładka                            |
| `column`       | `Column`        | Kolumna                                        |
| `row`          | `Row`           | Wiersz                                         |
| `grid`         | `Grid`          | Siatka                                         |
| `stack`        | `Stack`         | Układ pionowy                                 |
| `formfield`    | `FormField`     | Grupa pól z etykietą                           |
| `panelmenu`    | `PanelMenu`     | Menu w panelu                                  |
| `panelmenuitem`| `PanelMenuItem` | Element menu panelowego                        |

### Przykład:
```
Zgody section
 PodstawoweZgody formfield
  regulamin checkbox - Akceptacja regulaminu
```

---

## ✅ Tabele i dane (`ItemsContainerControl`)

| DSL         | Klasa C#     | Opis                               |
|-------------|--------------|------------------------------------|
| `datagrid`  | `Table`      | Tabela z wierszami i kolumnami     |
| `column`    | `DataColumnControl` | Kolumna tabeli              |

### Przykład:
```
Produkty datagrid
 Lp column
 Nazwa column
 Cena column
```

---

## ✅ Layout (`Layout`, `Header`, `Sidebar`, `Footer`)

| DSL        | Klasa C#   | Opis                                |
|------------|------------|-------------------------------------|
| `header`   | `Header`   | Górna część layoutu                 |
| `sidebar`  | `Sidebar`  | Lewa/prawa część layoutu            |
| `footer`   | `Footer`   | Dolna część layoutu                 |

### Przykład:
```
Header header
 LogoFirmy img datasource="https://..."
 Rejestracja link 

Sidebar sidebar
 column
  LogoFirmy img
  NazwaFirmy label
 panelmenu
  Analiza panelmenuitem
```

---

## 🔧 Atrybuty i rozszerzenia

- `- Opis` — tekst wyświetlany przy kontrolce
- `class="..."` — klasa CSS
- `width=...` — szerokość
- `datasource="..."` — źródło danych (dla `dropdown`, `img`, `link`)

---

## 🏗️ Mapowanie DSL → C#

| DSL              | Klasa C#                                 |
|------------------|-------------------------------------------|
| `form`           | `FormDefinition`                         |
| `textbox`        | `TextBox`                                |
| `checkbox`       | `CheckBox`                               |
| `dropdown`       | `ComboBox`                               |
| `img`            | `Image`                                  |
| `label`          | `TextBlock`                              |
| `link`           | `Link`                                   |
| `section`        | `Section`                                |
| `tabs` / `tab`   | `Tabs`, `Tab`                            |
| `datagrid`       | `Table`                                  |
| `column`         | `DataColumnControl`                      |
| `panelmenuitem`  | `PanelMenuItem`                          |

---

## 🧪 Przykład bez layoutu:

```
:PozyczkaOnline form
Pożyczka online h3

DaneFirmy section
 Dane firmy h5
 Nip textbox
 NumerTelefonu textbox
 AdresEmail textbox

Zgody section
 PodstawoweZgody formfield
  regulamin checkbox - Zgoda na regulamin
  przetwarzanie checkbox - Zgoda na przetwarzanie danych
```

## 🧪 Kompletny przykład:

```
:PozyczkaOnline form
Pożyczka online h3

DaneFirmy section
 Dane firmy h5
 Nip textbox
 NumerTelefonu textbox
 AdresEmail textbox

Zgody section
 Zgody h5

PodstawoweZgody formfield
 Podstawowe zgody label
 regulamin checkbox - Akceptacja regulaminu i polityki prywatności.
 przetwazanie checkbox - Zgoda na przetwarzanie danych osobowych zgodnie z obowiązującymi przepisami (np. RODO).

ZgodyMarketingowe formfield
 Zgody marketingowe label
 ZgodaTelefon checkbox - Wyrażam zgodę na kontakt telefoniczny w celu przedstawienia mi oferty produktów pożyczkowych firmy XYZ.
 ZgodaSMS checkbox - Wyrażam zgodę na otrzymywanie wiadomości SMS z informacjami o promocjach, ofertach specjalnych oraz nowościach produktów.
 ZgodaEmail checkbox -Wyrażam zgodę na otrzymywanie wiadomości e-mail zawierających informacje o produktach, aktualnościach oraz ofertach marketingowych.

Header header
 LogoFirmy img datasource="https://structura.agidot.eu/api/upload-image/get/image-13.png"
 g1
 Rejestracja link 
 DaneFinansowe link
 Realizacja link

Sidebar sidebar
 column
  LogoFirmy img datasource="https://structura.agidot.eu/api/upload-image/get/image-13.png"
  NazwaFirmy label
  g2
 panelmenu
  Analiza panelmenuitem
  Klienci panelmenuitem
 column
  g3 
  www.agidot.eu label
  Copyright Ⓒ 2025 label

```
