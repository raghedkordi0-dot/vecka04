## måndag

idag går jag igenom kapital 4 och bygger ett nätverk med 2 switchar och 4 datorer per switch, jag går igenom gördet själv uppgiften i boken. gjorde alla steg enligt boken och de har jag under filen nätverk,vlan och trunk.md
i steg 5- skulle jag pinga efter att ha tagit port VLAN 30 från allowed listan, vilket jag gjorde men fick svart request timed out, för vlan 30 fanns inte längre tillåtet på trunkporten på ena sidan, så vlan 30 trafik kan inte passera mellan switcharna.
jag körde därefter show interfaces trunk på både switcharna och och vlan 30 fanns inte med i allowed listan. vilket betyder att trafiken i vlan 30 inte kan går över trunken mellan switcharna och bevisar och förklarar varför pingen mellan datorerna gav request timed out.
när jag ändrade native vlan från 999 till 1 på ena switchen och behåll vlan 999 på den andra switchen fick jag varningen för NATIVE_VLAN_MISMATCH. det beror på att trunkportarna måste ha samma native vlan i både ändarna.
i steg 6- jag ändrade tillbaka native vlan 1 till native vlan 999 visar loggan ingenting vilket betyder att mismatchen försvann.
i steg -7 körde show spanning-tree vlan 30 på både switcharna. sw-nordvik 1 var root bridge för vlan 30. både switcharna hade samma STP priority så mac-addressen var avgörande för sw-nordvik 1 hade lägre mac-address och valdes därför automatiskt till root bridge.

## tisdag
jag går igenom python i boken och kontrollfrågorrna:

4.20 [typ 7 • Återblick] Räkna ut nätadress, broadcast och adressintervall för
192.168.1.128/26. (Kapitel 3)
blocksteget är 64
nätaddressen är 192.168.1.128
broadcast addressen är 192.168.1.191
antal tillgängliga addresser 62 för nät och broadcast addresser är reserverade.
tillgängliga addresser 192.168.1.129-190

4.21 [typ 7 • Återblick] Vad betyder adressen FF:FF:FF:FF:FF:FF, och vad gör switchen med en ram som har den som mottagare? (Kapitel 2)
det betyder att det är broadcast och switchen skicka ramen genom alla portar utom den porten ramen kom in på.

4.22 [typ 7 • Återblick] Vilken kolumn i show mac address-table avslöjar att en port ligger i fel nät? (Kapitel 2)
kolmunen vlan.