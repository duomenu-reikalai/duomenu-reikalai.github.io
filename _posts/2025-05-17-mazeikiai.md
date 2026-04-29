---
title: Ar Mažeikių vaikai yra narkomanai?
description: Antroji priešiško drono skrydžio per Lietuvą analizės dalis – apie garso įrašų iš vaizdo kamerų panaudojimą trajektorijos tikslinimui.
author: Statoras Datoras
date: 2025-05-17 22:33:00 +0300
tags: [švietimas, sveikata]
pin: false
math: false
mermaid: false
image:
  path: /assets/img/mazeikiai/thumbnail.png
  alt: ""
  no_bg: true
---

Būtent tokį įspūdį buvo galima susidaryti skaitant naujienų antraštes šią savaitę. Tačiau tiesa paskendo detalėse.

![..](/assets/img/mazeikiai/img1.png)



Tyrimo autoriai rezultatus skelbė pranešdami “teigiamų“ klasių procentą, pvz.: 
> “45.5 % **klasių** aptiktas tiesioginis sąlytis su psichoaktyviosiomis medžiagomis“.

Žiniasklaida, nesigilindama į skaičius, skubėjo skelbti:
> “Daugiau negu pusė **paauglių** turėjo sąlytį su itin pavojingomis medžiagomis“

Net ir tiksliai rezultatus citavusios žiniasklaidos priemonės daugeliui savo skaitytojų sukėlė įspūdį, kad narkotinių medžiagų paplitimas tarp **vaikų** yra 39.8%, 45.5%, 71.6%, 84.1%.


## Kaip išsiaiškinti tiesą?

### Ką mes žinome iš pranešimų spaudai

- buvo tirtos 9 Mažeikių rajono mokyklos, turinčios 5-ą, 6-ą, 7-ą ir 8-ą klases
- iš viso ištirtos 88 klasės
- tiesioginis sąlytis su PAM[^1] buvo aptiktas 40-yje **klasių**

[^1]: PAM – psichoaktyviosios medžiagos

Šaltinis: [nuoroda](https://mazeikiuvsb.lt/igyvendintas-mazeikiu-rajono-5-8-klasiu-mokiniu-salycio-su-psichoaktyviosiomis-medziagomis-patikrinimas/).


### Ko mes nežinome

- kokia dalis (%) **moksleivių** turėjo tiesioginį sąlytį su PAM
- ar buvo nors viena penktokų klasė, kurioje aptiktas tiesioginis sąlytis su PAM
- kiek moksleivių tirtose klasėse
- kuriose kurių mokyklų klasėse aptiktas tiesioginis sąlytis su PAM

Įdomu tai, kad sužinoję atsakymą į trečią klausimą, mes galime pasinaudoti statistiniais metodais ir rezultatus klasėms konvertuoti į rezultatus moksleiviams. Būtent rezultatai moksleiviams yra tai, kuo iš tiesų domisi visuomenė. Tad pamėginkime išsiaiškinti.

### Atvirų duomenų panaudojimas

Gausiuose Lietuvos atvirų duomenų rinkiniuose randame viską, ką mums reikia žinoti apie Mažeikių rajono mokyklas ir moksleivius:

![..](/assets/img/mazeikiai/img2.png)

Susiduriame su nauja problema: 5–8 klasių skaičius yra 93 (ne 88, kiek buvo tirta). Iš to kyla papildomas neapibrėžtumas – nežinome, kurios tiksliai klasės buvo tirtos, tad nežinome ir tikslaus moksleivių skaičiaus. Tačiau šią nežinojimo problemą nesunkiai išspręsime eigoje, naudodami simuliacijų metodą (*Bayesian inference*).

## Simuliacijų metodo paaiškinimas

Įsivaizduokime, kad turime daug paprastesnę situaciją: mokykloje yra dvi klasės ir 10 moksleivių; klasėje A mokosi 9 moksleiviai, klasėje B mokosi 1 moksleivis.

![..](/assets/img/mazeikiai/img3.png)

Mums reikia išsiaiškinti, kiek moksleivių turėjo sąlytį su PAM, tačiau dėl resursų ribotumo ir dėl moksleivių privatumo negalime tirti pačių moksleivių. Vietoj to galime tirti klasių durų rankenas (pigiau ir anonimiška), kurias moksleiviai neišvengiamai kasdien liečia.

Yra tik trys galimos tokio tyrimo, sudaryto iš dviejų rankenų patikrinimo, baigtys:

- 0 rankenų (klasių) turėjo sąlytį su PAM
- 1[^2] rankena (klasė) turėjo sąlytį su PAM
- 2 rankenos (klasės) turėjo sąlytį su PAM

[^2]: skelbiant rezultatus mums nepasakys, kuri konkrečiai klasė buvo teigiama, todėl baigtys yra trys (0, 1, 2), o ne keturios (0 klasių, klaseA, klasė B, abi klasės).

Sužinoję tyrimo atsakymą mes turėsime apskaičiuoti, koks yra labiausiai tikėtinas moksleivių, asmeniškai turėjusių sąlytį su PAM, skaičius.

### Žingsnis 1

Kadangi mokykloje mokosi 10 moksleivių, tikrasis mums rūpintis atsakymas (būtent apie moksleivius, o ne durų rankenas) gali turėti 11 reikšmių:

- **0** moksleivių turėjo sąlytį su PAM
- **1** moksleivis turėjo sąlytį su PAM
- …
- **10** moksleivių turėjo sąlytį su PAM

Kiekvienam iš šių 11-os realybės scenarijų mes priskirsime vienodą pradinę tikimybę (*prior probability*), nes vykdami į mokyklą neturime jokio pagrindo kažkuriuo iš scenarijų tikėti labiau nei kitais.

Kiekvienam iš scenarijų mes vykdysime po 100 simuliacijų, kurios sąlytį su PAM turėjusius vaikus **atsitiktinai** paskirstys tarp klasės A ir klasės B (nekeičiant klasių sudėties). Po kiekvienos iš simuliacijų įsivaizduosime, kad įvyksta mokyklos durų rankenų patikrinimas, tad kiekviena tokia simuliacija mums grąžins skaičių – kiek durų rankenų (klasių) buvo “teigiamos“.

Kadangi turime 11 scenarijų ir 100 simuliacijų kiekvienam jų, iš viso vykdysime 1,100 simuliacijų. Čia yra jų rezultatai:

![..](/assets/img/mazeikiai/img4.png)


Atkreikite dėmesį, kad vertikaliai simuliacijų skaičius visada sumuojasi į 100.

Nenuostabu, kad jeigu mokykloje iš tiesų yra tik vienas “teigiamas“ vaikas, cheminis tyrimas garantuotai suras lygiai vieną “teigiamą“ durų rankeną. Lygiai taip pat akivazdu, kad jeigu mokykloje nėra nei vieno “teigiamo“ vaiko, tyrimas garantuotai indikuos 0 “tegiamų“ rankenų, o jei visi vaikai yra “teigiami“, tai visuomet “teigiamos“ bus 2 rankenos.

Įdomesnė situacija yra kitais atvejais, pvz., jei mokykloje yra 2 “teigiami“ vaikai, tyrimas turi 80% tikimybę aptikti 1 “teigiamą“ rankeną, ir 20% tikimybę aptikti 2 “teigiamas“ rankenas. Neapibrėžtumas natūraliai kyla iš to, kad 2 “teigiami“ vaikai gali mokytis tiek toje pačioje klasėje, tiek dviejose skirtingose klasėse.

### Žingsnis 2

Ankstesnės iliustracijos rezultatus normalizuojame eilutėms: matematiškai perskaičiuosime taip, kad ne vertikalės sumuotųsi į 100, o horizontalės. Svarbu, kad kiekviena horizotalė išlaikytų tą pačią simuliacijų proporciją. Pavyzdys su viršutine (“2 rankenos“) eilute:

![..](/assets/img/mazeikiai/img5.png)

o tai yra lygu:

![..](/assets/img/mazeikiai/img6.png)

Veiksmus atlikę su kiekviena iš trijų eilučių gauname tokį vaizdą:

![..](/assets/img/mazeikiai/img7.webp)

Atkreipkite dėmesį, kad dabar kiekviena eilutė sumuojasi į 100, ir kiekvienos eilutės skaičius galima interpretuoti kaip tikimybes, išreikštas procentais: koks yra labiausiai tikėtinas “teigiamų“ vaikų skaičius. Įprastai kiekvienai eilutei išsirinktume ne patį didžiausią skaičių, o didžiausių skaičių grupę, kurios tikimybių suma sudaro, pvz., 80%. Tad dabar jau galime daryti išvadas:

![..](/assets/img/mazeikiai/img8.webp)

- Jeigu tyrimas aptiko **2** “teigiamas“ rankenas, labiausiai tikėtina, kad sąlytį su PAM mokykloje turėjo 5-10 vaikų (iš 10).
- Jeigu tyrimas aptiko **1** “teigiamą“ rankeną, labiausiai tikėtina, kad sąlytį su PAM mokykloje turėjo 1–5 vaikai (iš 10).
- Jeigu tyrimas aptiko **0** “teigiamų“ rankenų, akivaizdu, kad šios mokyklos vaikai su PAM sąlyčio neturėjo.

Pirmais dviem atvejais mes susiduriame su **statistiniu neapibrėžtumu**: atsakymą pateikiame kaip galimų atsakymų intervalą, pridurdami, kad tai yra “labiausiai tikėtina“ išvada, kuri turi ~20% tikimybę būti klaidinga.

Šis neapibrėžtumas – kaina, kurią sumokėjome už tai, kad atlikome tik 2 rankenų patikrinimus užuot patikrinę 10 mokinių. Neapibrėžtumas dažnai yra neišvengiamas, tačiau jei teisingai apskaičiuotas ir interpretuojamas – vis tiek yra naudingas.

Apibendrintai. Abu simuliacijos žingsniai ir jų rezultatai vienoje vietoje:

![..](/assets/img/mazeikiai/img9.png)

![..](/assets/img/mazeikiai/img10.png)

## Skaičiavimas simuliacijomis

Dabar jau skaičiuosime iš tikrųjų, pasiremdami turimais duomenimis apie tikrus Mažeikių rajono mokyklų PAM tyrimus.

### 1 žingsnis

Kiekvienoje simuliacijoje darysime dar šį tą, ko nebuvo mokomajame pavyzdyje: iš 93 mokyklų astitiktinai pasirinksime 88. Tokiu būdu į rezultatus įtrauksime ir neapibrėžtumą, kylantį iš šios nepilnos informacijos.

![..](/assets/img/mazeikiai/img11.png)

Kad geriau suprastume, kas čia vyksta, patyrinėkime paskutinį stulpelį iš iliustracijos dešinės pusės: kuomet vaikų, turėjusių sąlytį su PAM dalis yra lygi 10%.

![..](/assets/img/mazeikiai/img12.png)

Kaip reikėtų perskaityti šiuos rezultatus:

![..](/assets/img/mazeikiai/img13.png)

### 2 žingsnis

Kaip ir mokomajame pavyzdyje aukščiau, atliekame normalizavimą eilutėms:

![..](/assets/img/mazeikiai/img14.png)

Ir tai jau yra galutinis rezultatas. Kad geriau jį suprastume, pažiūrėkime į iliustracijos segmentą, esantį ties “teigiamų“ klasių sk. = 40:

![..](/assets/img/mazeikiai/img15.png)


Į dėžute apibrėžtą intervalą (2.2–2.8%) patenka didžioji dauguma (~90%) simuliacijų, todėl galime teigti, kad šis intervalas yra labiausiai tikėtinas.

## Rezultatai

Atsižvelgus į viską, ką žinome apie atliktą tyrimą ir Mažeikių rajono mokyklų sudėtį, galime teigti:

> Jeigu tyrimo autoriai iš 88-ių tirtų klasių 40-yje aptiko bent vieną moksleivį, turėjusį tiesioginį sąlytį su psichoaktyviosiomis medžiagomis, tai šio reiškinio paplitimas tarp moksleivių yra 2–3%., o ne 45.5% (40/88×100).

## Į ką neatsižvelgta, kas praleista

Mažeikių raj. savivaldybės vykdytas tyrimas turi ir kitų problemų, kurių statistiniais metodais išspręsti negalime:

- Daroma prielaida, kad PAM testo jautrumas ir specifiškumas yra 100%, t.y., kad jis niekada neklysta: visada aptinka, kuomet yra ką aptikti ir niekuomet neaptinka, kuomet nėra ko aptikti.
- Daroma prielaida, kad moksleiviai nebendrauja tarp klasių (nespaudžia rankų, nesidalina daiktais).

## Rekomendacija

- Atliekant tokį PAM tyrimą praverstų teigiama ir neigiama kontrolinės asmenų grupės.
- Pranešant tyrimo rezultatus būtina nurodyti, koks yra naudotų cheminių testų jautrumas ir specifiškumas, kad bent dalis visuomenės galėtų matematiškai įvertinti skelbiamų skaičių tikslumą.
- Jeigu taupant lėšas buvo atliekamas “kaupinių“ tyrimas (mėginys imamas iš moksleivių atskirai, bet tada sudedamas į vieną bendrą mėginį), tuomet autoriams derėjo atlikti čia aprašytus skaičiavimus ir visuomenei pranešti moksleivių procentą, o ne klasių procentą.
- Jeigu visgi buvo atliekami individualūs kiekvieno moksleivio tyrimai, tačiau nuspręsta rezultatus pranešti klasės lygiu, – tuomet buvo padaryta didelė komunikacinė klaida.

