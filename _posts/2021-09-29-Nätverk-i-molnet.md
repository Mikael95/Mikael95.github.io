# Webapplikationer i molnet

Följande inlägg kommer att gå ut på att övertyga sin CTO om att använda VPC(Virtual Private Cloud) och vad Azure Private.
Detta istället för privata interna servrar, hen vill ha full koll på data som skickas över nätet och vill därför ha egna servrar.

## Vad är Azure private link?

Azure Private Link kan du komma åt Azure PaaS-tjänster (till exempel Azure Storage och SQL Database)
och Azure-värdbaserade kundägda/partnertjänster via en privat slutpunkt i ditt virtuella nätverk.
Trafiken mellan ditt virtuella nätverk och tjänsten färdas via Microsofts stamnätverk. 
Det är inte längre nödvändigt att exponera tjänsten för det offentliga Internet. 
Du kan skapa en egen privat länktjänst i ditt virtuella nätverk och leverera den till dina kunder. 
Konfiguration och förbrukning med Azure Private Link är konsekvent i Azure PaaS-, kundägda och delade partnertjänster.

Detta ska alltså inte kunna läcka något känsligt vid överföring av data, jag tänte lägga fram några specifika fördelar med
private link med:

- Privat åtkomst till tjänster på Azure-plattformen: Anslut ditt virtuella nätverk till tjänster i Azure utan en offentlig IP-adress vid källan eller målet. 
  Tjänstleverantörer kan återge sina tjänster i sina egna virtuella nätverk och konsumenter kan komma åt dessa tjänster i sitt lokala virtuella nätverk. 
  Plattformen Private Link hanterar anslutningen mellan konsumenten och tjänsterna via Azure-stamnätverket.
- Lokala och peer-baserade nätverk: Få åtkomst till tjänster som körs i Azure från en lokal plats via privat ExpressRoute-peering, 
  VPN-tunnlar och peer-baserade virtuella nätverk med hjälp av privata slutpunkter.
- Skydd mot dataläckage: En privat slutpunkt mappas till en instans av en PaaS-resurs i stället för till hela tjänsten. 
  Konsumenter kan bara ansluta till den specifika resursen. Åtkomst till andra resurser i tjänsten blockeras. 
  Den här mekanismen ger skydd mot dataläckagerisker.
- Global räckvidd: Anslut privat till tjänster som körs i andra regioner. 
  Konsumentens virtuella nätverk kan finnas i region A och kan ansluta till tjänster bakom Private Link i region B.
  
## Vad är Virtual Private Cloud (VPC)?
  
VPC är mer eller mindre samma sak som det publika molnet fast utan den publika delen. Man kan göra samma saker som i det publika,
fast för att få ett virtual private cload måste företaget hyra en egen avskilld infrastruktur (single-tenant).

## Fördelar med VPC

- flexibilitet: den som hyr VPC:en har full kontroll över skalbarheten och kan skala upp och ner när det än behövs.
- Säkerhet: även om VPC molnet tekniskt sätt kör i det publika molnet så är det helt avskillt och begränsat till de rätta användarna.
- Kostnadseffektivt: som vanligt med moln så är det oftast billigare än att ha egen infrastruktur att underhålla.
- Tillgänglighet: VPC är mycket tillgängligt vanligtvis med låg down-time samtidigt som det är redundant.

## Källor

- [Microsoft](https://docs.microsoft.com/sv-se/azure/private-link/private-link-overview)
- [What is virtual private cload?](https://www.checkpoint.com/cyber-hub/cloud-security/what-is-vpc-virtual-private-cloud/)
