# Saugumo nustatymų valdymas gairelėmis

1. Kadangi Linux OS leidžia keliems vartotojams dirbti vienu metu, reikėjo būdo riboti prieigą prie kitų vartotojų failų. Failų ir katalogų priklausomybės požiūriu vartotojai skirstomi į savininkus ("**u**ser"), savininkų grupę ("**g**roup") ir kitus vartotojus ("**o**ther"), kurie nėra failo savininkai ir nepriklauso nurodytai failo savininkų grupei.
   
   Įvykdžius komandą
   
   ```bash
   $ ls -la
   ```
   
   Galima pamatyti informaciją apie kataloge esančius failus ir kitus katalogus, kam jie priklauso (t.y. kas yra savininkas ir kokia yra savininkų grupė), bei matyti failų ir katalogų gaireles (angl. "flags"), kurios nurodo, ką kiekviena gali daryti (skaityti 'r', keisti 'w', vykdyti 'x'). 

2. Sudarykime sau keistą problemą - failas yra, bet negalime pamatyti jo turinio, nors esame jo savininkai.
   Sukurkime failą ir patikrinkime jo gaireles bei turinį:
   
   ```bash
   $ echo "labas" > test.out
   $ ls -la test.out
   $ cat test.out
   ```
   
   Dabar uždrauskime sau skaityti tą failą, bet pamėginkime skaityti:
   
   ```bash
   $ chmod -r test.out
   $ ls -la test.out
   $ cat test.out
   ```
   
   Grąžinkime leidimą skaityti kitiems, bet ne sau:
   
   ```bash
   $ chmod og+r test.out
   $ ls -la test.out
   $ cat test.out
   ```
   
   Uždrauskime skaityti kitiems, bet leiskime sau:
   
   ```bash
   $ chmod og-r test.out
   $ chmod u+r test.out
   $ ls -la test.out
   $ cat test.out
   ```

3. Kad failo pavadinimas nesipainiotų, laikinai sukurtą failą *test.out* ištrinkite.
   
   

4. Norėdami pažiūrėti, kaip gairelės veikia kitų vartotojų požiūriu, pasinaudokime tuo, kad turime administratoriaus teises ir žinome, kad patys kūrėme vartotoją *uspecas*. Visų pirma įsitikinkite, kad *uspeco* namų katalogas yra ir jo negalite skaityti:
   
   ```bash
   $ ls -la /home           # žiūrime, kokios uspeco gairelės
   $ ls -la /home/uspecas
   $ chmod o+r /home/uspecas
   $ sudo chmod o+r /home/uspecas
   $ ls -la /home
   $ ls -la /home/uspecas
   $ sudo chmod o+x /home/uspecas
   $ ls -la /home
   $ ls -la /home/uspecas
   ```

5. Grąžinkite katalogo `/home/uspecas` gaireles į pradinį būvį.
   
   

6. Pažiūrėsime, kaip vykdymo gairelė 'x' įtakoja bash skripto failo vykdymą. Sukurkime failą `test.sh` (kadangi jis demonstracinis, tai parodau, kaip sukurti failą iš vykdymo eilutės) ir  pamėginkime jį įvykdyti keliais būdais:
   
   ```bash
   $ echo "echo hi \$USER" > testas.sh
   $ cat testas.sh
   echo hi $USER
   $ bash testas.sh
   $ ls -la testas.sh
   $ ./testas.sh
   ```
   
   Pažymėkime, kad failą galima vykdyti ir išbandykime suteiktą leidimą:
   
   ```bash
   $ chmod u+x testas.sh
   $ ./testas.sh
   ```
   
   Nustatyta vykdymo gairelė neturi įtakos failo tiesioginiam
   paleidimui `bash` komandos pagalba (tačiau yra kitų - akivaizdžiai
   nematomų pasekmių, apie kurias mokinsimės vėliau):
   
   ```bash
   $ bash testas.sh
   ```
   
   

7.  Šiek tiek pasimokinome failo gairelių.





Peržiūrėta 2022.10.06 d.
