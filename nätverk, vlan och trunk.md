jag bygger ett nätverks i Cisco packet tracer som består av 2 switchar och 4 datorer per switch. samt en specifik port länk mellan switcharna som jag använder som trunk.
jag börjar med att ändra hostname på både switcharna för att underlätta processen.

<img width="832" height="456" alt="Screenshot From 2026-09-14 14-51-03" src="https://github.com/user-attachments/assets/b27922a4-e603-4af4-a43a-a0acde05ed2c" />

jag skapar vlan 10 EKONOMI, vlan 20 KONTOR, vlan 30 GUEST, vlan 99 DRIFT och vlan 999 NATIVE.
vlan 999 är tänkt vara native vlan på trunken för otaggad trafik medan taggad trafik går över de andra vlan.
sedan kontrollerar jag att att vlan togs med kommandot show vlan brief

<img width="1504" height="748" alt="Screenshot From 2026-09-14 15-01-42" src="https://github.com/user-attachments/assets/464cb334-ef35-4c38-b904-245224abe251" />

sedan gör jag switchporten till accessport och bestämma vilken port som ska tillhöra vilket VLAN.

<img width="1504" height="748" alt="Screenshot From 2026-09-14 15-11-48" src="https://github.com/user-attachments/assets/3f523e9d-73e1-4cc0-a9e4-c25e6a945294" />

nu när allt är klart, börjar jag med trunk konfigurationen på både switcharna där konfigurerar jag gi0/1 som trunkport eftersom det är länken mellan switcharna. sen tilllåtar jag vlan 10,20,30,99 att gå över trunken medan vlan 999 förblir som native vlan

<img width="1504" height="748" alt="Screenshot From 2026-09-14 15-35-32" src="https://github.com/user-attachments/assets/a7fc32ea-235b-4d39-8725-2648f71234db" />

efter detta, kontrollerar jag kommunikationen mellan datorerna genom att pinga, detta gör jag genom att ge den ena datoren på SW-Nordvik-1 en ip address 192.168.1.12 och datoren på andra sidan 192.168.1.13  och pingar från den aoch får bevis på att VLAN 10 fungerar över trunken.
bilden visar att trafiken kunnat gå från VLAN 10 på ena switchen över trunklänken till VLAN 10 på andra switchen.

<img width="700" height="735" alt="Screenshot From 2026-09-14 17-00-34" src="https://github.com/user-attachments/assets/91c0c32a-7a0d-4e62-a513-c58b6ff1fb4a" />


Vlan 20, 30 och 99 fungerar också, kontrollerat det på sammat sätt:


<img width="711" height="738" alt="Screenshot From 2026-09-14 17-11-08" src="https://github.com/user-attachments/assets/3e886f4e-0a6c-4acc-96ab-01cf7bcd4151" />

<img width="711" height="738" alt="Screenshot From 2026-09-14 17-14-37" src="https://github.com/user-attachments/assets/84adfad5-de69-4879-a565-49584144616d" />

<img width="701" height="725" alt="Screenshot From 2026-09-14 17-17-12" src="https://github.com/user-attachments/assets/3168b0cc-e057-4886-a9f6-ac7885564f3a" />

sen kontrollerade jag show spanning-tree vlan 10 och såg att både switcharna hade samma priority. men SW-Nordvik-1 hade lägre MAC-address och valdes per automatiskt till root bridge.

<img width="1414" height="739" alt="Screenshot From 2026-09-14 17-25-35" src="https://github.com/user-attachments/assets/a6e0c3d9-f894-4ace-80c2-902aef0b6419" />
