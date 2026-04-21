V rámci druhého projektu v kurzu Testovací akademie firmy Engeto jsem měla za úkol otestovat projektové REST API pro správu studentů. Ověřovala jsem metody GET, POST, PUT a DELETE se zaměřením na funkčnost, validaci vstupů a také konzistenci dat v databázi, ke které jsem měla přístup.

Testováním jsem odhalila zásadní nedostatky ve validaci i práci s daty. API často povoluje nevalidní vstupy (typicky například nesprávné datové typy, prázdné či duplicitní hodnoty) a v některých případech data samo, bez upozornění, upravuje, nebo nahrazuje defaultními hodnotami.

Problémy, které považuji za nejvíc kritické, jsem objevila u metod PUT a DELETE - zde dochází k nevyžádaným změnám dat (například přepis pole isEuCitizen) a v případě DELETE nejsou záznamy reálně odstraněny z databáze i přesto, že API vrací úspěšný status 200 OK.

API jako takové je skvěle připraveno k testování studenty kurzu. Vykazuje nekonzistentní logiku, nemá dostatečně ošetřeny  chybové stavy a má velice nestabilní a nespolehlivé chování během aktualizace i mazání dat.



Na základě revize dokumentace bylo upřesněno, že schema StudentCreate neobsahuje žádná required pole a všechny atributy jsou definovány jako nullable. Scénáře s chybějícími nebo null hodnotami proto nebyly dále vedeny jako aplikační defekty, ale jako ověření skutečného chování API. Jako defecty zůstaly evidovány pouze případy, které odporují validační logice, formátu dat nebo vedou k nekonzistentní manipulaci s uloženými hodnotami.

