#G

1. Plats där information förvaras permanent. Man kan förvara t.ex. priser i en textfil eller JSON-fil men för stora
   mängder data är databas bättre. Består av en eller flera filer på en disk.
2. Språk som används för att kommunicera med databaser. Man kan t.ex. hämta data ur tabeller genom att skriva SELECT.
3. Tabell är uppbyggd av rader och kolumner och samlar information av samma typ av sak, tex produkter. Kolumn är en typ
   av information t.ex. pris medan rad ger all information om en specifik produkt.
4. Identifierar unikt en rad. Gör det t.ex. lätt att radera en rad.
5. Connectar info mellan tabeller. T.ex. om man har customers table och orders table och foreign key kan då vara
   customers.id.
6. Man kanske vill ta bort ett köp men inte hela kunden.
7. Att man inte ordnar i tabeller utan bara lägger in data. Det kan organiseras t.ex. i JSON-filer
8. En produktkatalog för den uppdateras ofta och då slipper man tänka på relationer mellan tabeller
9. SELECT * FROM person;
10. SELECT first_name, last_name FROM person;
11. SELECT first_name, last_name, income FROM person WHERE income > 30000;
12. SELECT * FROM person WHERE dob < '1990-01-01';
13. SELECT first_name, last_name, income FROM person ORDER BY income DESC;
14. SELECT COUNT (*) FROM person;

#VG

1. Konsekvenserna om en banköverföring avbryts efter att pengarna dragits från det första kontot kan vara att de inte
   sätts in på kontot som skulle ha de och att pengarna försvinner och att det blir fel i systemet.

En kund kan alltså förlora sina pengar och mottagaren får inte betalt, vilket kan leda till exempelvis
förseningsavgifter. Pengar försvinner ur systemet så bankens system blir fel också eftersom man inte kan se var pengarna
tagit vägen och den totala summan inte längre stämmer.

En transaktion kan förhindra att det sker genom att den avbryter att pengar dras om de inte sätts in på något konto.
Detta eftersom transaktioner fungerar genom principen att göra allt eller inget och databasen rättar felet om det skulle
avbrytas genom att ändra tillbaka datan, så kallad rollback. Detta kallas atomicity. Först när båda stegen lyckats
sparas ändringen permanent. Det är pålitligt även vid till exempel systemkrascher. Har man gjort commit ska datan finnas
kvar ändå. Detta kallas durability. Om kraschen sker innan commit så görs en rollback när man startar om. Transaktioner
säkerställer också consistency, till exempel om det inte finns något konto att sätta in pengar på stoppas det och kontot
kan inte ha ett negativt belopp. Transaktioner kan även ha olika isolationsnivåer. Till exempel kan hög isolationsnivå
göra så att om två personer klickar köp på samma biobiljett så går det inte att köpa den om den redan är tagen även om
det bara skiljer till exempel 0.000001 sekunder.

2. Jag har valt att redogöra för när SQL-databas respektive NoSQL-databas är lämplig i chatt. Fördelarna med
   NoSQL-databas är att man inte behöver hålla på med tabeller och relationer mellan dem och det brukar inte behövas i
   chatt eftersom meddelandena inte behöver kopplas till varandra. Man kan lagra meddelandena som till exempel JSON
   liknande dokument med MongoDB. Det blir också högre hastighet om man slipper hålla reda på relationer mellan tabeller
   och det är viktigt när användarna chattar med varandra. Det är även enkelt att använda många servrar (horisontell
   skalning) istället för en kraftfullare med NoSQL (vertikal skalning), vilket gör att man slipper köpa dyrare och
   kraftfullare RAM-minne till en server.

SQL-databas kan vara bra när man till exempel ska hantera medlemmar i gruppchattar, till exempel om man vill veta vilken
användare som är medlem i vilken grupp. Man kopplar ihop grupp-id och användar-id så att rätt användare får tillgång
till rätt grupp-id och då är det viktigt att det blir rätt om till exempel en användare ska tas bort. Denna säkerhet ger
SQL genom främmande nycklar och ACID. ACID är 4 egenskaper hos transaktioner:
atomicity = till exempel när användare raderas ska användaren och dess kopplingar till gruppchatten tas bort helt eller
inte alls consistency = till exempel får koppling i gruppchatten får inte peka på en användare som inte finns
isolation = till exempel om två personer ändrar behörigheter samtidigt krockar det inte durability = till exempel om en
gruppchatt skapats och sparats försvinner inte den vid en krasch

Det bästa är nog att ha en chatt som inkluderar både SQL-databaser och NoSQL-databaser så att man får det bästa från
båda delarna.


