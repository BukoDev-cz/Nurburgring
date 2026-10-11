# Nordschleife Simulátor

Realistická závodní hra v prohlížeči, odehrávající se na okruhu inspirovaném Nürburgringem Nordschleife. Celá hra je **jeden soubor HTML** (`index.html`), běží bez instalace a po načtení i bez internetu. Rozhraní je v češtině.

> Hru jsem vytvořil s pomocí Claude. Trať, vozy, textury i zvuk jsou generované v kódu, žádné externí modely ani obrázky.

## Jak hru spustit

- **Na počítači:** stáhni `index.html` a otevři ho dvojklikem v Chrome, Edge nebo Firefoxu.
- **Na webu (GitHub Pages):** nahraj soubor do repozitáře jako `index.html`, v *Settings → Pages* zvol větev `main` a složku `/ (root)`. Hra pak poběží na `https://<uživatel>.github.io/<repozitář>/`. Na mobilu ji můžeš v Chrome přidat na plochu (menu ⋮ → *Přidat na plochu*).

Doporučení: aktuální Chrome nebo Edge s hardwarovou akcelerací WebGL. Na mobilu hraj nejlépe na šířku.

## Co hra umí

- **Fyzika:** vlastní čtyřkolový model (přenos zatížení, tření pneumatik, ABS, kontrola trakce, ESC, aerodynamika, teplota a opotřebení pneumatik, poškození).
- **Trať:** celý okruh s převýšením, klopením zatáček, obrubníky, zábradlím a lesem; pojmenované zatáčky se zobrazují před vozem.
- **Vozy:** Hot Hatch (přední pohon), GT Coupé (zadní pohon) a GT3 Race (aerodynamika, vysoký přítlak).
- **Počasí a denní doba:** slunečno, zataženo, mokro, liják a soumrak. Mění se přilnavost i vzhled.
- **Grafika:** PBR materiály, odlesky na laku, proceduralní textury asfaltu, trávy a zábradlí, stíny, ACES tone mapping a volitelné efekty kamery (bloom, vinětace, zrno, rozostření při rychlosti). Tři úrovně kvality.
- **Pohledy:** kokpit s pohybem hlavy při zatáčení a brzdění a otřesy od obrubníků, kapota, nárazník a kamera za vozem.
- **Zvuk a hudba:** syntetizovaný motor, pneumatiky, vítr a déšť, k tomu hudební smyčka s ztlumením při jízdě.
- **Měření kol:** časy kol, mezičasy, nejlepší kolo a duch nejlepšího kola.

## Výzvy, rekordy a ukládání

- V menu je sekce **Výzvy** s 11 úkoly (první kolo, čisté kolo bez nárazu, 100 km, kolo pod 9:00 / 8:00 / 7:30, kolo za deště, výhra nad lehkým / středním / těžkým botem, závod v multiplayeru). Splněná výzva se oznámí a zůstane zaškrtnutá.
- **Nejlepší kola** se ukládají zvlášť pro každý vůz (osm nejlepších časů s datem).
- Hra si pamatuje poslední zvolený vůz, počasí, soupeře, počet kol, asistenty, kameru, kvalitu grafiky a hlasitost hudby.
- Všechno se ukládá jen v prohlížeči (`localStorage`), nikam se neposílá. Smazáním dat webu se pokrok smaže.
- Na dotykových zařízeních se jako výchozí zvolí **nízká kvalita**, aby hra běžela plynule. Vyšší kvalitu můžeš zapnout v menu.

## Závod proti botovi

V menu v sekci **Soupeř** zvol obtížnost (lehký, střední, těžký) a počet kol. Bot jede po trati podle rychlostního profilu a reaguje na kolize. Během závodu můžeš přepnout kameru na soupeře klávesou **V** (na mobilu tlačítko *Soupeř*).

## Evoluce botů

Tlačítko **Evoluce botů** v menu otevře samostatný režim, ve kterém se učí 100 botů najednou (neuroevoluce):

1. Nakresli prstem nebo myší uzavřenou trať (nebo zvol *Náhodná trať*).
2. V úpravách můžeš přidat **překážky**, **mosty** (úsek trati vedený přes jinou část) nebo trať překreslit. Nástroj přepínáš tlačítkem *Nástroj*.
3. Stiskni **READY ▶ spustit**. Každý bot vidí 7 senzorních čar a řídí se neuronovou sítí.
4. Bot, který se dotkne okraje, překážky nebo jede špatným směrem, se změní na ducha a stojí. Ostatní jedou dál.
5. Když skončí všichni, vznikne nová generace z nejlepších a vše se opakuje. Kdo dojede kolo, spustí hlášení **FINISH**.

Kliknutím vybereš bota a kamera ho sleduje. K dispozici jsou přepínače rychlosti, zobrazení senzorů všech botů a kamery (přehled, nejlepší, vybraný).

## Multiplayer

Multiplayer funguje **jen když hru otevřeš přímo v Claude** (jako artefakt) a ostatní hráči mají k artefaktu přístup. Zadáš přezdívku a kód místnosti, hráči se zobrazí na trati a po načtení všech klikne každý na **Ready**, teprve pak začne odpočet. Při kolizích se auta srážejí. Ve verzi mimo Claude (GitHub Pages, soubor v počítači) multiplayer vypnutý je, ostatní režimy fungují.

## Ovládání

**Klávesnice**

| Klávesa | Akce |
|---|---|
| W / ↑ | plyn |
| S / ↓ | brzda, po zastavení couvání |
| A D / ← → | řízení |
| Q / E | podřadit / zařadit vyšší (ruční řazení) |
| Mezerník | ruční brzda |
| C nebo 1–4 | kamera: kokpit, kapota, nárazník, za vozem |
| V | sledování soupeře |
| R | vrátit se na trať |
| H | přepnutí přístrojů |
| M | zvuk |
| P / Esc | pauza a nastavení |
| Myš | rozhlížení v kokpitu |

**Dotyk (mobil):** levým palcem táhni posuvník řízení, pravým drž *Plyn* a *Brzdu*. Tlačítka vedle ovládají asistenty, řazení, kameru, reset a pauzu. Ovládání (klávesnice / dotyk) se přepíná v menu a pamatuje se.

## Technické informace

- Jediný soubor `index.html`, bez serveru a bez sestavování; obsahuje i knihovnu **three.js r128** a hudbu.
- Veškerá 3D grafika (trať, vozy, stromy, textury) je procedurální. Fyzika běží na pevném kroku 240 Hz.
- Nastavení (ovládání, kvalita, hlasitost hudby, efekty) se ukládá do `localStorage` prohlížeče.
- Zdrojový kód je v souboru jen zmenšený (minifikovaný). Kdo soubor stáhne, kód přečíst může. Chceš-li kód chránit, nezveřejňuj ho.

## Poznámky a omezení

- Hra je **nezávislé fanouškovské dílo**, žádný oficiální produkt ani licencovaný okruh. Tvar trati je přibližný.
- Výkon se liší podle zařízení. Na slabším mobilu zvol nízkou kvalitu a vypni efekty kamery.
- Hudba je smyčka z vlastního tracku autora. Pokud ji chceš použít jinde, zkontroluj si práva.

## Licence

Doplň podle sebe (například MIT pro kód). Bez uvedené licence zůstávají všechna práva autorovi.

## Kariéra
V menu nahoře: 12 událostí ve 4 sériích (Nováček → Klubová → Profesionálové → Legenda Ringu). Série se odemkne po vyhrání 2 událostí v předchozí. Za výhru dostaneš kredity (čistý závod bez nárazu +25 %), za prohru malou útěchu. V garáži kupuješ vozy (GT Coupé, GT3 Race; vyšší série je vyžadují) a vylepšuješ motor, pneumatiky, brzdy a hmotnost (3 stupně). Postup se ukládá v prohlížeči.

### Více soupeřů
Kariérní události mají 1 až 8 soupeřů. U závodů s více boty stačí top 2–3 (u finále jen vítězství), výplata podle místa: 1. místo 100 %, 2. 70 %, 3. 50 %. Ve volné jízdě si počet soupeřů (1, 2, 3, 5, 8) zvolíš v menu u Soupeře. Klávesou V (na mobilu tlačítko Soupeř) přepínáš sledování jednotlivých botů.
