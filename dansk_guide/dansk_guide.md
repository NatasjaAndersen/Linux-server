# Opsætning af linux server via Digital Ocean
*Først og fremmest vil jeg gøre opmærksom på at jeg på ingen måde er professionel til Linux servere, den viden jeg har er baseret på undervisning og research* 

Indholdsfortegnelse:
- 1 Oprettelse på Digital Ocean
- 2 Download af putty
- 3 Opsæt putty med Digital Ocean og dit projekt
- 4 Opsætning af mysql (Database drevne applikationer)
- 5 Bugfixing

Indholdsfortegnelsen vil hjælpe dig med at springe rundt til det emne der er relevant for lige netop *dig* 

-------------------------

## 1 Oprettels epå Digital Ocean (DG)
Det første du gør er at gå ind på hjemmesiden digitalocean.com når du er derinde vil du se en blå knap hvor du kan oprette dig osm bruger (sign up), følg trinene i oprettelses processen og du er 'good to go' 
Vær dog opmærksom på at du *skal* angive dine kortoplysninger, nogle kan være imod dette men alternativerne er få men du kan prøve at tage et kig på "Herokuu" hvis det er, jeg vil dog kun fokusere på Digital Ocean. 

Når du er oprettet kan du trykke på den grønne knap "Create" der vil komem en dropdown menu frem og i den vælger du "Create new Droplet" en droplet er det samme som en server. 

Nu vil der komme en masse valgmuligheder jeg vil anbefale at du kører med "centOS" 6.9 X32 Næste skridt er at vælge størrelsne på serveren, hvis du bare skal uploade små projektet er 5$/month mere end rigeligt til dig. Du springer bare punktet "Bloakge Storage" over for nu, det næste du skal er at vælge en host placering, vælg gerne det der er tættest på din lokation, tallene er ligemeget det er bare hvilket server nummer din server vil være hostet fra. Du springer bare over punkterne "Select additional options" og "Add SSH keys"
Til sidst navngiver du abre din droplet, default settings er nogle mærkelige navne som du burde undgå, antal er naturligvis op til dig men jeg skal som regel kun bruge en droplet. 

Når du ahr gjort det vil du blive først over til en side hvor du kan se alle dine droplets, derinde vil din nye droplet blive tændt på default når den er færdig med at oprette. 

Hvis du vil direkte videre til punkt to skal du bare være din droplet være tændt og gå videre til punkt 2. 

---------------------------

# 2 Download putty
Det næste skridt i processen er at downlaode et program der hedder putty, det er en lille terminal der er nødvendig for at kunne udføre diverse kommandoer og til at forbinde din droplet med dit projekt på Github. 

Du går ind på følgende link: http://www.putty.org/
Derinde trykker du på det første link du ser I den tredje fase trykker du på (sreenshot på vej)

Nu følger du bare installationsprocessen indtil den er installeret.

Når putty er installeret skal du lgie tilbage til Digital Ocean og hente ip adressen på din droplet, det gør du ved at gå ind på digitalocean.com -> log ind -> fanen droplets -> tryk på navnet på din droplet (eller den droplet du vil tilføje hvis du har flere droplets) -> Tjek at dropleten står på "on" 
Hvis alle tingene er som de skal være kan du se en ip adresse der hedder ipv4 helt til venstre den ip kopiere du og indsætte i den øverste input linje i din putty applikation. 

Derefter givre du din ip et navn (det vil jeg anbefale i hvert fald) når du har gjort det trykker du på knappen "save" helt til højre når det er gjort kan du trykke på "load" og derefter "open" i bunden.

----------------------

# 3 Opsæt putty med dg og dit projekt
Det første der sker når du har åbnet din putty konsole r at den beder om et brugernavn her er default altså bare "root" dernæst vil den spørge dig om et førstegangs-kodeord som er blevet sendt til den email du har oprettet dig med på digitalocean

Når du ha råbnet den email vil du se en lang kode dne kopierer du ved at markere den med musemarkøren og så højreklikke og tryk 'kopier' eller trykke ctr + c, derefter går du ind i din putty konsol igen og paster den ind ved at højreklikke én gang med din mus. 
OBS! Du kan *IKKE* se koden, det er altså ikke fordi der er noget galt men fordi det er sikkerhed, når du har sat koden in trykker du på enter tasten, herefter spørger den om et UNIX kodeord og der indsætter du den samme kdoe som du lige har sat ind forinden.

Derefter spørger putty dig om en kdoe som *DU* laver, det er altså denne kdoe du fremover skal logge ind med og ikek den du har hentet fra emailen, så husk ast skriv koden ned. 

Nu er du klar til at opsætte selve serveren, det allerførste vi skal have fat i er en simpel editor, du kan sagtens nøjes med en simpel en som hedder nano, den første kommando du skriver vil altså være 
```js
yum install nano
``` 
Efter et øjeblik kommer der en masse ting frem du bare skal sige ja til (Det gør du ved at skrive "y" og trykke enter)

Det næste du skal have sat op er mysql
```js
yum install mysql-server
```
Når serveren er installeret er det en god idé at starte den så du er sikker på at det hele kører som det skal, det gør du med følgende kommando
```js
service mysqld start
```
Hvis du vil stoppe eller genstarte mysql serveren skriver du bare "stop" eller "restart" i stedet for "start"

Nu skal mysql konfigueres, det bliver gjort med følgende kommando
```js
sudo /usr/bin/mysql_secure_installation
```
sudo står for superuser hvis du skulle undre dig. 
Herinde vil der komme en masse ting frem med hensyn til opsætning at mysql serveren 

Processen vil blandt andet spørge om dit password det er altås det password du logger ind på putty med (det som du selv lavede i starten) derefter vil den spørge om et password til mysql *HER ER DET SUPER VIGTIGT AT DU ANGIVER ET KODEORD* du kan sagtens bruge det samme kodeord som du har brugt til at logge ind på putty med, bare husk at skriv det ned. 
Derefter vil der blive spurgt om mysql skal fjerne den anonyme bruger der er oprettet, her er det en god idé at skrive "y" for yes, den vil også spørge om du vil gøre så man kun kan logge ind fra localhsot, det er lidt op til dig om du vil det ene eller det andet y for ja og n for nej, derefter vil der blive spurgt om tets databasen skal fjernes der plejer jeg altid at skrive y for ja.
sidst spørger den om du vil restarte og der skriver du bare yes for at bekræfte. 

Næste skridt er at installere node.js i putty konsollen. 
Det første du skriver er
```js
yum install epel-release
``` 
Derefter skriver du
```js
yum install nodejs
```
DErnæst
```js
yum install npm
```
Og sidst
```js
npm install -g n
```
Nu er node installeret men den vil have brug for en opdatering, måden du gør det på er at skrive
```js
n lts
```
Derefter skriver du bare 
```js
n
```
Nu burde din node være opdateret, så skal du lgie have genstartet din putty terminal, det gør du enten ved at skrive
```js
exit
```
Eller ved at trykke på x'et i toppen af putty vinduet

Derefter åbner du putty igen (henviser øverst i guiden hvis du har glemt hvordan man åbner putty)

Det næste der skal installeres er et modul der hedder pm2, det er en manager til ndoe.js applikationer hvor du både kan starte og stoppe dem
```js
npm install -g pm2
```
Det er en god idé at køre pm2 ved en startup process det gør du ved at skrive
```js
pm2 startup
```
Jeg vil enbefale at du bruger startup kommandoen som noget af det første hver gang du åbner et putty projekt

Det næste du skal bruge er git (så du kan forbinde til dine github repositories)
```js
yum install git
```
Derefter skal du konfiguere dine git data
```js
git config --global user.name "DIT GITHUB BRUGERNAVN HER"
```
Derefter det samme med din email
```js
git config --global user.email "DIN GITHUB EMAIL HER"
```
Det er altid en god idé at tjekke din konfiguration det er heldigvis super nemt det eneste du skal skrive er
```js
nano ~/.gitconfig
```
Hvis alt er som det skal være trykker du bare på ctr + x, det vil lukke nano editoren ned og føre dig tilbage til putty terminalen.

Det er en god idé at oprette et nøglesæt til din forbindelse
```js
ssh-keygen -t rsa
```
Når nøglen er genereret vil der komme en sjov lilel firkant op med nogle forskellige symboler i, hvis du ser den har du gjort det rigtigt og kan fortsætte til næste skridt
```js
nano ~/.ssh/id_rsa.pub
```
Denne kommando vil åbne nano editoren igen hvor du nu vil kunne se en meget lang linje. Du bruger piletasten til at navigere den grønne markør frem og tilbage, kør nu denne markør til højre og lav et linebreak (tryk enter) dette gør du indtil du har splittet din nøgle så meget op at du kan se den hele i putty vinduet.

Når det er gjort markere du alle tegnene når det hele er markeret går du in på din github profil og trykker på "settings" derinde trykker du på "SSH and GPG keys" inde i det vinduer trykker du på den grønne knap der hedder "new SSH key"
derinde sætter du din nøgle ind med ctr + v husk at fjerne dine linebreaks igen så nøglen bliver samlet. 
Når det er gjort trykekr du på "save" og så er du klar til at gå tilbage til putty konsollen

Det er en god idé at oprette en root mappe så alle dine filer ikke bar eliger og flyder rundt i sleve roden på din putty server, det er heldigvis super nemt at oprette nye mapper med en simpel kommando
```js
mkdir ~/MAPPENAVN
```
mkdir er egentlig bare "make directory" og der angiver du mappens navn jeg ville kalde den noget i stil med "projekter" eller "opgaver" eller noget andet sigende for en oversigts mappe.

Når du har givet din mappe et navn bruger du en bestemt kommando til at navigere rundt
```js
cd ~/MAPPENAVN
```
Nu er du inde i mappen som du har angivet, og det er her du skal klone dine github repositorities fra (hvis du vil undgå at de ender i roden)

Det første du gør er at skrive klone kommandoen
```js
git clone git@github.com:DITGITHUBBRUGERNAVNHER/REPOSITORYNAVNHER
```
Hvis dit projekt ikke har en database laver du bare ændringer i projektet i dit visual studio code (eller anden editor) jeg tage rudgangspunkt i at du har visual studio code som editor
Når du har lavet ændringer trykker du på din fork ude i venstre side der kan du se en oversigt over alle dine ændringer, der klikker du på det lille + ikon på de filer du ønsker at sende til Github, derefter trykker du på de tre ... og vælger punktet "commit staged" derefter trykker du igen på de tre ... og klikker på "push" når det er gjort går du tilbage til din putty og skriver
```js
git pull git@github.com:DITBRUGERNAVN/REPOSITORYNAVN master
```
Det er vigtigt du husker "master" til sidst så putty ved hvilken branch den skal commite til ellers vil den ikke sende dit commit afsted og dermed ikke opdatere projektet på din server. 

For at starte din server i putty skriver du enten 
```js
pm2 start all
```
eller
```js
node NAVNPÅSERVERFIL
```
F.eks
```js
node app
```
- Hvis dit projekt er delt op i en frontend og backend del vil jeg enbefale dig at du tænder for din backend del først for at undgå adress already in use errors.

Men hvis dit projekt har en database skal du følge trinene i næste punkt.

# 4 Opsætning af database med putty
Hvis du har en database på din localhost så skal du lige igennem et par ekstra tring, det tager heldigvis ikke så lang tid :)

Det første er at sikre sig a mysql'en er sat op, det gør du ved at gå til roden i din putty konsol (Skriv "cd .." og det bliver du ved med at skrive indtil du er i roden)
```js
mysql -p
```
-p står for password
Nu bliver du bedt om at angive dit mysql password og det er det du angav da du installerede mysql helt i starten.
Når du er derinde kan du se der står "mysql_" og det er det rigtige

Derefter skriver du 
```js
GRANT ALL ON *.* TO 'root'@'%';
```
Når denne kommando er sendt har man sagt at brugeren "root" skal have alle tilladelser uanset host destination, % tegnet representeret hosts.

Nu skal der sættes et password op til root brugeren (Jeg vil anbefale at du bruger det samme som du har gjort i hele processen)
```js
SET PASSWORD FOR 'root'@'%' = PASSWORD('SKRIVDITKODEORDHER');
```
Nu er du faktisk færdig med at sætte mysql'en op

Nu skal du have downloadet et program der hedder mysql workbench, du kan også bruge en anden applikation men jeg bruger selv mysql workbench da det er relativt simpelt. (link til download kommer senere)

Når du har din workbench indstalleret og åbent vil du formegentlig allerede se en firkantet kasse der hedder loalhsot men hvis du ikke har det trykker du på det lille runde + ikon, dernæst kommer der en dialog bok frem med nogle forskellige indstillinger, det du skal kigge på er ip adressen hvis den strater med 127 er det din lokale og så går du bare ned i bunden og trykekr på "save" 

Nu burde du kunne se en grå firkantet boks på forsiden af workbench, den kasse dobbeltklikker du på og den vil tage dig ind på dine databaser som du har liggende lokalt (localhost) 
Inde i det panel finder du den database der hører til dit projekt (i venstre side af vinduet) og klikker på database navnet
Når det er gjort klikker du på "server" helt oppe i toppen af vinduet og dernæst på "data export" for at eksportere din database, inde i det nye vindue tryker du bar epå "start export" nede i højre hjørne. 

Efter et øjeblik vil du få en besked om at din database er importeret.
Nu trykker du så på det lille hus i toppen af workbench vinduet så du ender på forsiden igen, her trykker du på det lille runde + og inde i det opsætningsvindue vil du igen se ip adressen der starter med 127, nu skal den ændres til at være din digital ocean droplet ip adresse (gå til dine droplets på digitalocean.com hvis du har glemt den) og indsæt den, derefter trykker du bare på "save"

Hvis alt er som det sakl vil du nu se to grå bokse på forsiden en med din localhsot og en med det navn du lige har oprettet en med, nu dobbeltklikekr du på den og det password du bliver bedt om at indtaste her er altås passwordet til din mysql som du angav da du indstallerede mysql i din putty! 

Når du er inde klikker du på det lille database ikon næsten helt øverst af workbench vinduet. (Den hedder new scheme) giv den helstd et samme navn som den database du lige har eksporteret.
Når det er gjort vil du se den nye database til venstre i listen den trykker du på og går så op i server og klikker på "data import" derefter kan du se et felt med nogle mappe navne for enden af den bjælke er der tre ... tryk på dem og gå ind i dokumenter og en mappe der hedder "dumps" der vælger du den database du lige har eksporteret, når det er gjort trykker du start import. Og bam! Nu har du din database forbundet.

Gå tilbage til din putty og skriv "service mysqld start" for at være sikker på det hele kører. 

Det kan godt være du er nødt til at genstarte din Putty server process. 

# 5 Bugfixes
Nu er det jo sådan at der kan opstå fejl når man arbejder med teknisk udstyr, og det samme er altså tilfældet med putty og workbench. Jeg vil liste nogle af de fejl jeg har oplevet med nogle løsnings forslag som du/I forhåbentlig kan bruge ellers må du/I meget gerne kontakte mig så kan vi jo prøve at løse det sammen? 

### 1) Du får en fejl ved database import (Så dine tabeler der indeholder fields med "CURRENT_TIMESTAMP") 

*Hvis du oplever en importfejl i den grad er det faktisk en alvorlig fejl da nogle af dine tabeller lige pludselig ikke bliver importeret, for at løse det er du nødt til at gå tilbage til den database der ligger på localhost, når du har valgt den database går du op i fanen der hedder "query 1" og indsætter følgende kommando*
```js
ALTER TABLE `Tabelnavn`  
MODIFY kollonnenavn TIMESTAMP 
DEFAULT CURRENT_TIMESTAMP 
NOT NULL;
```
*Tabelnavn er naturligvis den/de tabeller du ikke kan få importeret. 
Du kan dog ikke vælge flere tabeller af gangen så hvis det er flere tabeller er du altså nødt til at køre kommandoen en gang for hver tabel der har problemet.*

*Når du har gjort dette ved alle de tabeller der er påvirket går du op i server igen og trykker på data export. 
Nu går du så ind i din online database og markere den databse du allerede har og går op i server og derefter data import, der trykekr du igen på de tre ... og vælger den nyeste eksporterede database i dump mappen, når det er gjort så tryk på databasen i højre vindue og tjek at dine tabeller er der.* 
*Hvis de er det trykker du på "start import" når det er gjort burder du kunne se dine tabeller i databaen (Du kan tjekke det ved at gå idn i menuen til venstre og klikke på din database og så på "tabeller")*

------------------------
### 2) Jeg får en fejl om at mit projekt allerede er in use i min putty 

*Hvis du får en adress already in use fejl så prøv at kør med "pm2 stop all" og derefter "pm2 start all" eller hvis du bruger node så kør "pm2 stop all" og derefter naviger hen til din backend del og skriv "node NAVNPÅSERVERFIL" og derefter det samme i din frontend (-Hvis dit projekt er delt op i frontend og backend)*

----------------------------
### 3) Jeg kan ikke forbinde til min workbench når jeg prøver at klikke på den grå boks får jeg en connection error

*Hvis du får en connection error i Workbench så gå til din putty konsol og skriv* 
```js
service mysqld start
```
*De fleste connection errors i workbench er faktisk fordi folk glemmer at tænde for deres mysql i putty konsollen*
