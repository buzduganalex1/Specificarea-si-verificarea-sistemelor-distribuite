# Project Specifications

## Description

Model an online shop using cpn tools. The model has to be comprise of three modules:
- Client
- Delivery
- Admin

## Client

- Permite inregistrarea de clienti noi, login penru clienti deja inregistrati
- Baza de date clienti (utilizand liste): pentru fiecare client se retin, pe langa datele personale, comenzile clientului respectiv
- Un client pot vedea produsele dintr-o anumita categorie (nu si cantitatea disponibila), poate alege sa cumpere diverse cantitatati dintr-un produs (acest lucru va fi posibil daca exista cantitatea necesara) si poate alege un anumit tip
de livrare. In functie de tipul de livrare ales, la costul produselor se adauga
costul de livrare. In comanda se va include si o adres de livrare. Se va genera o
camanda cu aceste date, care va avea un anumit identificator. Comanda poate fi
confirmata sau anulata de catre client. Pentru a plasa o comanda, un client
trebuie sa fie logat. Dupa ce comanda este confirmata, va fi trimisa la sistemul
de livrare si va ajunge intr-o stare “in asteptare” in pagina client. Dupa ce
livrarea este finalizata, comanda va fi finalizata.
- Orice client logat isi poate vedea comenzile anterioare

## Delivery

- Modulul preia comenzile de la clienti. Dupa livrare, notifica atat clientii cat si
modulul Admin (care va adauga produsele din comanda intr-o lista cu comenzi
finalizate) iar apoi va salva comanda
- Modulul permite realizarea de interogari (cate comenzi au fost livrate la o
anumita adresa, cate comenzi au fost livrare unui anumit client).

## Admin

- permite interogari asupra stocului de produse
- permite interogari asupra bazei de date cu comenzile finalizate (de exemplu:
cate produse dintr-o anumita categorie a cumparat un anumit client, valoarea
totala a produselor cumparate de un client, cate produse de un anumit tip au
fost vandute in total). Interogarile vor fi modelate prin tanzitii, parametrii
interogarilor vor fi selectati din locatii in care se gasesc valorile posibile)
- calculeaza veniturile generate (prin comenzi finalizate)
- permite update asupra stocului de produse (se selecteaza o anumita cantitate si
un anumit produse) sau se pot elimina anumite produse din stoc (se selecteaza
cantitatea care va fi eliminata)

## Implementation description

