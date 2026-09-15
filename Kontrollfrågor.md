4.1 [typ 1 • Kontrollfråga] Vad är skillnaden mellan ett VLAN och ett IP-nät?
Vlan handlar om vilka portar som hör ihop och ligger i lager 2 medan IP-nät handlar om addresser och ligger i lager 3.

4.2 [typ 1 • Kontrollfråga] Vad skiljer en access-port från en trunk?
En access port är witch port som tillhör ett enda VLAN där sitter datorer medan trunk port bär flera VLAN samtidigt och där sitter andra switchar eller en router.

4.3 [typ 1 • Kontrollfråga] Vilka två rader behövs för att lägga en port i ett VLAN, och
varför räcker inte den ena?
switchport mode access och switchport access vlan <nummer> utan den första kommadot står switchen i sitt automatiska läga och väljer något annat än det man tänkt sig.

4.4 [typ 1 • Kontrollfråga] Vad gör taggningen, och var i nätet finns taggen?
tagging gör att det står VLAN nummret i ramen och går bara på trunken mellan switcharna och till router. Tagging står i ramen när ramen går in i en trunk och försvinner innan ramen går ut på acces porten.

4.5 [typ 1 • Kontrollfråga] Varför ska en trunk aldrig kopplas till en dator?
för datoren förstår inte taggade ramar.

4.6 [typ 1 • Kontrollfråga] Vad är native VLAN, och vad är standardvärdet?
Det är det VLAN som går otaggat över trunken. stadard är 1 på cicso switchar.

4.7 [typ 1 • Kontrollfråga] Vad går fel om två switchar har olika native VLAN?
loggen visar duplex mismatch RECV_PVID_ERR och då hamnar otaggad trafik från det äna nätet i det andra nätet. spanning tree stänger av de två vlanen på porten.

4.8 [typ 1 • Kontrollfråga] Vad förhindrar STP, och hur gör den det?
spanning tree protokoll förhindrar att ramar går runt i en cirkel för evigt. genom att stänga av de portar som skulle skapa cirkeln och öppna dem igen om den öppna vägen går sönder.

4.9 [typ 1 • Kontrollfråga] Vad betyder BLK i show spanning-tree, och vad ska du göra åt det?
det betyder att stp stängde porten avsiktligt. man ska inte göra något åt det för porten är reserv.att dra ur kabeln är ett säker sätt att ta ner nätet.

4.10 [typ 1 • Kontrollfråga] Vad händer om du kör switchport trunk allowed vlan två gånger med olika nummer?
då har man bara den VLAN som man skrev sist

4.11 [typ 1 • Kontrollfråga] Skriv den engelska termen för vart och ett av följande: access-port, trunk, taggning, native VLAN och root bridge. Provet frågar efter dem.
access-port, trunk, tagging, native VLAN and root bridge

4.12 [typ 2 • Räkneövning] Nordviks fyra VLAN delar 192.168.1.0/24 i fyra lika stora delar. Räkna ut nätadress, gatewayadress, första och sista användbara adress samt broadcastadress för alla fyra. Använd schemat i bilaga C och skriv svaret som en tabell.
VLAN          Vad          Nät                   adresser          Gateway              Broadcastaddress
10            Kontor       192.168.1.0/26        1-62              192.168.1.1          192.168.1.63
20            Ekonomi      192.168.1.64/26       65-126            192.168.1.65         192.168.1.127
30            Gäst         192.168.1.128/26      129-190           192.168.1.129        192.168.1.191
99            Drift        192.168.1.192/26      193-254           192.168.1.193        192.168.1.255

4.13 [typ 2 • Räkneövning] Ekonomiavdelningen växer till 70 datorer. Räcker /26? Räkna ut hur många adresser en /26 ger, hur många av dem som går att använda, och vilken mask som skulle behövas i stället.
/26 ger 62 tillgängliga addresser har ekonomi avdelningen vuxit till 70 då räcker inte /26 så går man till /25 som får plats till 128 addresser varav 126 tillgängliga addresser för de 2 reserverade är en till nätaddressen och en till broadcastaddress.

4.14 [typ 3 • Läs utdatan] Här är ett utdrag från två switchar som är hopkopplade. Datorer i VLAN 20 når inte varandra över trunken, men VLAN 10 fungerar. Vad är fel?
SW-Nordvik-1# show interfaces trunk
Port
Gi0/24
Vlans allowed on trunk
10,30,99
SW-Nordvik-2# show interfaces trunk
Port
Gi0/24
Vlans allowed on trunk
10,20,30,99
problemet är att show interfaces trunk visar olika allowed listor i dem två switcharna. switch 1 visar att vlan 10,30,99 finns med i allowed och vlan 20 saknas medan på switch 2 visas vlan 10,20,30,99. det betyder att trunken kommer inte tillåta vlan 30 att går över trunken.
man kan rätta till det genom att gå till conf t i switch 1 och slå kommandot switchport mode trunk sen switchport trunk allowed vlan add 20.

4.15 [typ 3 • Läs utdatan] Här är ett utdrag från en switch. En dator i port Gi0/5 får ingen adress från DHCP-servern, som sitter i VLAN 10. Vad frågar du efter härnäst?
SW-Nordvik-1# show vlan brief
VLAN Name
Status
Ports
---- -------------------------------- ---------
,→ -------------------------------
1
default
active
Gi0/5,
,→ Gi0/6
10
KONTOR
active
Gi0/7,
,→ Gi0/8
20
EKONOMI
active
Gi0/9
Fråga vilket VLAN porten ligger i. Gi0/5 står under VLAN 1, inte under VLAN 10 där DHCP-servern finns.

4.16 [typ 4 • Konfigurationsövning] Skriv den fullständiga konfigurationen för trunkenmellan SW-Nordvik-1 och SW-Nordvik-2. Den ska bära VLAN 10, 20, 30 och 99, ha
native VLAN 999 och inte förhandla om läget. Skriv varje rad, i rätt ordning, från configure terminal till end.
enable
conf t
interface gigabitethernet <nummer>
switchport trunk encapsulation dot1q
switchport mode trrunk
switchport trunk native vlan 999
switchport trunk allowed vlan 10,20,30,99
switchport nongotiate
exit
end

4.17 [typ 4 • Konfigurationsövning] Port Gi0/11 till Gi0/14 på SW-Nordvik-1 ska läggas i VLAN 20 och slippa vänta på STP när en dator kopplas in. Skriv konfigurationen
med så få rader som möjligt.
enable
conf t
ineterface range gi0/11 - gi0/14
switchport mode access
switchport access vlan 20
spanning-tree portfast
exit
end

4.18 [typ 5 • Översätt kravet] Nordviks gäster ska kunna nå internet men ingenting annat i huset. Ekonomiavdelningen ska ha ett eget nät som varken kontoret eller gästerna
når. Driftpersonalen ska kunna nå switcharna från sitt eget nät. Skriv den VLAN- konfiguration switchen behöver, och säg vilken del av kravet du inte kan lösa med VLAN ensamt.
det behövs tre vlan till gäster, ekonomi och drift. svaret till resten av frågon kommer i kommande kapitalen.

4.19 [typ 6 • Förklara för någon annan] Skriv fem meningar till en kollega som aldrig hört talas om VLAN, där du förklarar varför två datorer i samma switch ändå inte kan nå varandra.
Vlan delar upp en fysisk switch i flera nätverk.
två datorer kan därför vara anslutna till samma switch men ändå tillhör olika vlan.
om datorerna ligger i olika vlan kan switcharna inte skicka trafik direkt mellan dem.
för att trafik ska kunna gå mellan olika vlan behövs trunk.
vlan använda för att seperera olika grupper av enheter och göra nätverket mer organiserat och säkert.
