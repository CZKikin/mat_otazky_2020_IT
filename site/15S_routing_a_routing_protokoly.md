# 15. Směrování a směrovací protokoly

## Statické směrování
Při statickém (též neadaptivním) směrování nejsou za běhu stanice záznamy ve směrovací tabulce nijak aktivně měněny. Může je do ní zapsat správce počítače (typicky podle údajů poskytnutých správcem příslušné počítačové sítě) nebo jsou do tabulky zapsány při startu počítače. Záznamy mohou být uchovány v konfiguračním souboru (v Microsoft Windows pak v registrech) nebo poskytovány například pomocí protokolu DHCP.

Statické směrování typicky používají koncové stanice nebo routery v malých počítačových sítích (LAN), protože záznamy není nutné v průběhu činnosti zařízení měnit a nebo proto, že jsou záznamy jednoduché.

## Dynamické směrování
Dynamické (adaptivní) směrování průběžně reaguje na změny v počítačové síti (přidávání nebo odebírání podsítí) a přizpůsobuje jim obsah směrovací tabulky. Podle způsobu, jakým si jednotlivá zařízení vyměňují informace o změnách v počítačové síti, lze dynamické směrování rozdělit do několika základních skupin (které se vzájemně prolínají a kombinují). Pro distribuci těchto informací mezi směrovači se používají různé směrovací protokoly.


## Dva typy protokolů

### Distance vector protocols
Distance vector protocols advertise their routing table to all directly connected neighbors at regular frequent intervals using a lot of bandwidth and are slow to converge. When a route becomes unavailable, all router tables must be updated with that new information. The problem is with each router having to advertise that new information to its neighbors, it takes a long time for all routers to have a current accurate view of the network. Distance vector protocols use fixed length subnet masks which aren’t scalable.

### Link state protocols
Link state protocols advertise routing updates only when they occur which uses bandwidth more effectively. Routers don’t advertise the routing table which makes convergence faster. The routing protocol will flood the network with link state advertisements to all neighbor routers per area in an attempt to converge the network with new route information. The incremental change is all that is advertised to all routers as a multicast LSA update. They use variable length subnet masks, which are scalable and use addressing more efficiently.

## Interior Gateway Routing Protocol (IGRP)
Interior Gateway Routing Protocol is a distance vector routing protocol developed by Cisco systems for routing multiple protocols across small and medium sized Cisco networks.

It is proprietary which requires that you use Cisco routers. This contrasts with IP RIP and IPX RIP, which are designed for multi-vendor networks.

IGRP will route IP, IPX, Decnet and AppleTalk which makes it very versatile for clients running many different protocols. It is somewhat more scalable than RIP since it supports a hop count of 100, only advertises every 90 seconds and uses a composite of five different metrics to select a best path destination.

Note that since IGRP advertises less frequently, it uses less bandwidth than RIP but converges much slower since it is 90 seconds before IGRP routers are aware of network topology changes. IGRP does recognize assignment of different autonomous systems and automatically summarizes at network class boundaries. As well there is the option to load balance traffic across equal or unequal metric cost paths.

- Distance Vector
- Routes IP, IPX, Decnet, Appletalk
- Routing table adverisements every 90 seconds
- Metric: Bandwith, Delay, Reliability, Load, MTU Size
- Hop count: 100
- Fixed lenght subnet masks
- Summarization on Network class address
- Load balancing across 6 equal or unequal cost paths
- Metric calculation = destination path minimum bandwidth * delay (usec)
- Split horizon
- Timers: Invalid (270s), Flush (630), Holddown (280s)

## Enhanced Interior Gateway Routing Protocol (EIGRP)

Enhanced Interior Gateway Routing Protocol is a hybrid routing protocol developed by Cisco systems for routing many protocols across an enterprise Cisco network.

It has characteristics of both distance vector routing protocols and link state routing protocols. It is proprietary which requires that you use Cisco routers. EIGRP will route the same protocols that IGRP routes (IP, IPX, Decnet and Appletalk) and use the same composite metrics as IGRP to select a best path destination.

As well there is the option to load balance traffic across equal or unequal metric cost paths. Summarization is automatic at a network class address however it can be configured to summarize at subnet boundaries as well. Redistribution between IGRP and EIGRP is automatic as well. There is support for a hop count of 255 and variable length subnet masks.

- Advanced Distance Vector
- Routes IP, IPX, Decnet, Appletalk
- Routing Advertisements: Partial When Route Changes Occur
- Metrics: Bandwidth, Delay, Reliability, Load, MTU Size
- Hop Count: 255
- Variable Length Subnet Masks
- Summarization on Network Class Address or Subnet Boundary
- Load Balancing Across 6 Equal or Unequal Cost Paths (IOS 11.0)
- Timers: Active Time (180 sec)
- Metric Calculation = destination path minimum BW * Delay (msec) * 256
- Split Horizon
- LSA Multicast Address: 224.0.0.10
 
## Open Shortest Path First (OSPF)
Open Shortest Path First is a true link state protocol developed as an open standard for routing IP across large multi-vendor networks. A link state protocol will send link state advertisements to all connected neighbours of the same area to communicate route information. Each OSPF enabled router, when started, will send hello packets to all directly connected OSPF routers.

The hello packets contain information such as router timers, router ID and subnet mask. If the routers agree on the information they become OSPF neighbours. Once routers become neighbours they establish adjacencies by exchanging link state databases. Routers on point-to-point and point-to-multipoint links (as specified with the OSPF interface type setting) automatically establish adjacencies. Routers with OSPF interfaces configured as broadcast (Ethernet) and NBMA (Frame Relay) will use a designated router that establishes those adjacencies.

### Areas
OSPF uses a hierarchy with assigned areas that connect to a core backbone of routers. Each area is defined by one or more routers that have established adjacencies. OSPF has defined backbone area 0, stub areas, not-so-stubby areas and totally stubby areas. Area 0 is built with a group of routers connected at a designated office or by WAN links across several offices. It is preferable to have all area 0 routers connected with a full mesh using an Ethernet segment at a core office. This provides for high performance and prevents partitioning of the area should a router connection fail. Area 0 is a transit area for all traffic from attached areas. Any inter-area traffic must route through area 0 first. Stub areas use a default route to forward traffic destined for an external network such as EIGRP since the area border router doesn’t send or receive any external routes. Inter-area and intra-area routing is as usual. Totally stubby areas are a Cisco specification that uses a default route for inter-area and external destinations. The ABR doesn’t send or receive external or inter-area LSA’s. The not-so-stubby area ABR will advertise external routes with type 7 LSA. External routes aren’t received at that area type. Inter-area and intra-area routing is as usual. OSPF defines internal routers, backbone routers, area border routers (ABR) and autonomous system boundary routers (ASBR). Internal routers are specific to one area. Area border routers have interfaces that are assigned to more than one area such as area 0 and area 10. An autonomous system boundary router has interfaces assigned to OSPF and a different routing protocol such as EIGRP or BGP. A virtual link is utilized when an area doesn’t have a direct connection to area 0. A virtual link is established between an area border router for an area that isn’t connected to area 0, and an area border router for an area that is connected to area 0. Area design involves considering geographical location of offices and traffic flows across the enterprise. It is important to be able to summarize addresses for many offices per area and minimize broadcast traffic.

- Link State
- Routes IP
- Routing Advertisements: Partial When Route Changes Occur
- Metric: Composite Cost of each router to Destination (100,000,000/interface speed)
- Hop Count: None (Limited by Network)
- Variable Length Subnet Masks
- Summarization on Network Class Address or Subnet Boundary
- Load Balancing Across 4 Equal Cost Paths
- Router Types: Internal, Backbone, ABR, ASBR
- Area Types: Backbone, Stubby, Not-So-Stubby, Totally Stubby
- LSA Types: Intra-area (1,2) Inter-area (3,4), External (5,7)
- Timers: Hello Interval and Dead Interval (different for network types)
- LSA Multicast Address: 224.0.0.5 and 224.0.0.6 (DR/BDR) Don’t Filter !
- Interface Types: Point to Point, Broadcast, Non-Broadcast, Point to Multipoint, Loopback

## Integrated IS-IS
Integrated Intermediate System – Intermediate System routing protocol is a link state protocol similar to OSPF that is used with large enterprise and ISP customers. An intermediate system is a router and IS-IS is the routing protocol that routes packets between intermediate systems. IS-IS utilizes a link state database and runs the SPF Dijkstra algorithm to select shortest paths routes. Neighbor routers on point to point and point to multipoint links establish adjacencies by sending hello packets and exchanging link state databases. IS-IS routers on broadcast and NBMA networks select a designated router that establishes adjacencies with all neighbor routers on that network. The designated router and each neighbor router will establish an adjacency with all neighbor routers by multicasting link state advertisements to the network itself. That is different from OSPF, which establishes adjacencies between the DR and each neighbor router only. IS-IS uses a hierarchical area structure with level 1 and level 2 router types. Level 1 routers are similar to OSPF intra-area routers, which have no direct connections outside of its area. Level 2 routers comprise the backbone area which connects different areas similar to OSPF area 0. With IS-IS a router can be an L1/L2 router which is like an OSPF area border router (ABR) which has connections with its area and the backbone area. The difference with IS-IS is that the links between routers comprise the area borders and not the router. Each IS-IS router must have an assigned address that is unique for that routing domain. An address format is used which is comprised of an area ID and a system ID. The area ID is the assigned area number and the system ID is a MAC address from one of the router interfaces. There is support for variable length subnet masks, which is standard with all link state protocols. Note that IS-IS assigns the routing process to an interface instead of a network.

- Link State
- Routes IP, CLNS
- Routing Advertisements: Partial When Routing Changes Occur
- Metric: Variable Cost (default cost 10 assigned to each interface)
- Hop Count: None (limited by network)
- Variable Length Subnet Masks
- Summarization on Network Class Address or Subnet Boundary
- Load Balancing Across 6 Equal Cost Paths
- Timers: Hello Interval, Hello Multiplier
- Area Types: Hierarchical Topology similar to OSPF
- Router Types: Level 1 and Level 2
- LSP Types: Internal L1 and L2, External L2
- Designated Router Election , No BDR

## BGP

rder Gateway Protocol is an exterior gateway protocol, which is different from the interior gateway protocols discussed so far. The distinction is important since the term autonomous system is used somewhat differently with protocols such as EIGRP than it is with BGP. Exterior gateway protocols such as BGP route between autonomous systems, which are assigned a particular AS number. AS numbers can be assigned to an office with one or several BGP routers. The BGP routing table is comprised of destination IP addresses, an associated AS-Path to reach that destination and a next hop router address. The AS-Path is a collection of AS numbers that represent each office involved with routing packets. Contrast that with EIGRP, which uses autonomous systems as well. The difference is their autonomous systems refer to a logical grouping of routers within the same administrative system.

An EIGRP network can configure many autonomous systems. They are all managed by the company for defining route summarization, redistribution and filtering. BGP is utilized a lot by Internet Service Providers (ISP) and large enterprise companies that have dual homed internet connections with single or dual routers homed to the same or different Internet Service Providers. BGP will route packets across an ISP network, which is a separate routing domain that is managed by them.

The ISP has its own assigned AS number, which is assigned by InterNIC. New customers can either request an AS assignment for their office from the ISP or InterNIC. A unique AS number assignment is required for customers when they connect using BGP. There are 10 defined attributes that have a particular order or sequence, which BGP utilizes as metrics to determine the best path to a destination.

Companies with only one circuit connection to an ISP will implement a default route at their router, which forwards any packets that are destined for an external network. BGP routers will redistribute routing information (peering) with all IGP routers on the network (EIGRP, RIP, OSPF etc) which involve exchange of full routing tables. Once that is finished, incremental updates are sent with topology changes. Each BGP router can be configured to filter routing broadcasts with route maps instead of sending/receiving the entire internet routing table. 

## RIPv2
Routing Information Protocol version 2 (RIPv2), was a common LAN routing protocol in the '90s, 
but is rapidly fading away in production networks. RIPv2 suffered from scalability issues due to 
a relatively low maximum hop count of 15 routing devices. 
Compared to more modern dynamic routing protocols, RIPv2's methods for selecting optimal 
routes and the substantial convergence time it takes to recalculate paths renders it nearly obsolete. 
Today, the only reason you might run across a network running RIPv2 is either that the 
network is very old and in serious need of an upgrade or the network 
is running cheaper, consumer-grade routing hardware that can only support RIP.

## Cena cesty
To je číslo v rozsahu 1 až 65535, přiřazené ke každému rozhraní směrovače. Čím menší číslo, tím má cesta lepší metriku a bude tedy více preferována. Standardně je ke každému rozhraní přiřazena cena automaticky odvozená z šířky pásma daného rozhraní. Požívá ho například protokol OSPF

## Metrika
Metrika sítě se používá pro nalezení optimální trasy z jedné sítě do druhé. Pokud dojde směrovači paket, který má routovat do sítě, která však k němu není připojena a router propojuje více sítí, paket může router přeposlat více branám. Pak se rozhoduje podle směrovací tabulky. V tabulce má udánu adresu sítě a síťovou masku - dvojici, která jednoznačně určuje síť - spolu s bránou, kterou je síť dosažitelná a metrikou - číslem, které udává cenu spojení. Pokud je cest více, vybírá se to s nižší metrikou. Pokud nefunguje, vybírá se ze zbytku spojení to s nejnižší metrikou atd.

Metriku lze stanovit různými způsoby. Zvolený způsob určuje optimalizační hledisko. Například lze přiřazovat velkou metriku pomalým (málo propustným) a malou rychlým (hodně propustným) trasám. Hlediskem je pak rychlost. Stejně tak lze použít délku trasy v metrech, počet routování (tedy počet routerů na trase) apod.

## Router on the stick
Router on the stick se používá pokud máme na switchi nastavené VLANy a chceme, aby si uživatlé z různých VLAN byly schopni mezi sebou posílat zprávy. Jelikož switch nemá žádné prostředky k tomu, aby byl schopen zprávy posílat mezi VLANy, musíme použít zařízení, které pracuje na L3 vrstvě, v tomto případě router. Uživatel pak pošle zprávu z dané VLANy na router a ten ji pošle zpátky do VLANy jiné.

## NAT
NAT je způsob úpravy síťového provozu procházejícího přes router přepisem zdrojové nebo cílové IP adresy, případně i hlaviček protokolů vyšší vrstvy (např. číslo portu u TCP, UDP, ICMP Query ID u ICMP  atd.). NAT může být implementován softwarově na běžném počítači (např. v jádře Linuxu pomocí iptables/netfilter)  nebo může být realizován přímo ve firmware či hardware routeru. NAT se většinou používá pro přístup více počítačů z lokální sítě do Internetu prostřednictvím jediné veřejné IP adresy (viz gateway). NAT však znemožňuje přímou komunikaci mezi klienty (end–to–end spojení) a může snížit rychlost přenosu.

## Příkazy pro konfiguraci směrovačů Cisco
### Administrativní mód
Po připojení ke směrovači cisco se musíte přepnout z uživatelského (>) do privilegovaného (#) módu.
```
cisco> enable
cisco#
```
Je možné využít i zkratky `ena`

### Konfigurační mód
```
cisco# configure terminal
cisco(config)#
```
Je možné použít i zkratky `conf term`.


### Změna názvu zařízení
Směrovače se nemusí jmenovat pouze obecně, ale jejich název může být i napovídající. Např. pokud chcete směrovač přejmenovat na C1, musíte zadat.
```
cisco(config)# hostname C1
C1(config)#
```

### Testování směrování
Směrovače umožňují také rychlou kontrolu směrování, např. příkazy ping či traceroute. Může se stát, že směrovaní nefunguje popř. že uděláte překlep. V tom případě musíte čekat, dokud příkaz sám n eskončí, Ctrl+C zde nefunguje. Funguje ale jiná zkratka. Ctrl+Shift+61)

### Přirazení IP adresy
V konfiguračním módu zvolíme rozhraní a tomu přidělíme IP (IPv6) adresu.
```
cisco(config)# interface fastEthernet 0/0
cisco(config-if)# ip address a.a.a.a m.m.m.m
cisco(config-if)# ipv6 address aaaa:aaaa:aaaa:aaaa:aaaa:aaaa:aaaa:aaaa/pp
```
Dále je nutné rozhraní FE0/0 zapnout pro komunikaci.
```
cisco(config-if)# no shutdown
```
Nyní máme na rozhraní FE0/0 IP adresu a.a.a.a s maskou m.m.m.m (prefixem pp) a rozhraní je zapnuto pro komunikaci. Do konfiguračního módu se vrátíme příkazem exit.
```
cisco(config-if)# exit
cisco(config)#
```
Všimněte si, že příkaz shutdown je negován příkazem no shutdown, potřebujete-li odstranit něco z konfigurace, pak použijte příkaz no a příkaz, kterým jste něco špatně nastavili.
Pro ověření funkčnosti daného rozhraní můžete v administrativním módu použít příkaz ping.
```
cisco# ping a.a.a.a
cisco# ping aaaa:aaaa:aaaa:aaaa:aaaa:aaaa:aaaa:aaaa
```

### Statické směrování
Záznamy pro přímo připojené sítě se tvoří automaticky při jejich konfiguraci. Pro ostatní sítě použijte následující příkazy v konfiguračním módu.
```
cisco(config)# ip route a.a.a.a m.m.m.m g.g.g.g
cisco(config)# ip route a.a.a.a m.m.m.m FastEthernet 0/0
cisco(config)# ipv6 route aaaa:aaaa:aaaa:aaaa::/pp gggg:gggg:gggg:gggg:gggg:gggg:gggg:gggg
```
Síť a.a.a.a s maskou m.m.m.m bude připojena přes bránu g.g.g.g nebo do sítě na rozhraní FastEthernet 0/0.
Pro zobrazení stávajících směrovacích tabulek použijte příkaz v administrativním módu
```
cisco# show ip route
cisco# sh ip route
cisco# show ipv6 route
```
### IPv6
Směrovače Cisco po startu nesměrují zprávy IPv6. To je nutné nejprve zapnout příkazem
```
cisco(config)# ipv6 unicast-routing
```

### Překlad adres
Rozhraní, které je připojeno do lokální sítě se názývá inside, rohraní připojeno do vnější sítě (Internet) se nazývá outside. V konfiguračním režimu nastavíme tyto příznaky pro potřebaná rozhraní.
```
cisco(config)# interface FastEthernet 0/1
cisco(config-if)# ip nat inside
cisco(config-if)# exit
cisco(config)# interface FastEthernet 0/0
cisco(config-if)# ip nat outside
cisco(config-if)# exit
```

Následně musíme nastavit samotný dynamický překlad adres a definovat rozsahy, které určují co se bude překládat na co.
```
cisco(config)# ip nat pool jmenoRozsahu b.b.b.b e.e.e.e prefix-length X
cisco(config)# ip nat inside source list Y pool jmenoRozsahu overload
cisco(config)# access-list Y permit a.a.a.a w.w.w.w
```
Pool (rozsah vnějších adres) s názvem jmenoRozsahu obsahuje adresy od b.b.b.b až po e.e.e.e ze sítě, jejíž maska (prefix) je X. List Y je číslo seznamu v paměti směrovače, obvykle se používá číslo 7. V posledním příkazu definujeme, které adresy se mohou účastnit překladu, adresa a.a.a.a s inverzní maskou w.w.w.w bude v seznamu Y povolena. Pro každou síť, jejíž prvky budou procházet NATem, je nutné vložit záznam do access-listu.


### Port forwarding
Aby směrovač umožnil přístup k službám počítačů za NATem, je nutné použít statický NAT. Pokud je funkce statického NATu omezena pouze na nějaký port protokolů 4. vrstvy, pak se někdy tato funkce nazývá port forwarding.
```
cisco(config)# ip nat inside source static tcp i.i.i.i p o.o.o.o p extendable
```
Adresa i.i.i.i je ip adresa stroje ve vnitřní síti, p je port, o.o.o.o je ip adresa směrovače na vnějším rozhraní, na kterém přijímá packety.

### DHCP server
Pro nastavení DHCP serveru musíme zadat následující sekvenci příkazů.
```
cisco(config)# ip dhcp pool name
cisco(dhcp-config)# domain-name sub.example.com
cisco(dhcp-config)# dns-server p.p.p.p s.s.s.s t.t.t.t
cisco(dhcp-config)# network n.n.n.n m.m.m.m
cisco(dhcp-config)# default-router a.a.a.a
cisco(dhcp-config)# exit
```
p.p.p.p značí primární DNS server, stejně s.s.s.s a t.t.t.t značí sekundární a ternární DNS server. a.a.a.a je IP adresa výchozí brány, kterou bude DHCP nabízet.
Pokud potřebujeme vyloučit některé adresy z přidělovaného rozsahu, použijeme
```
cisco(config)# ip dhcp excluded-addresses a.a.a.a
cisco(config)# ip dhcp excluded-addresses b.b.b.b e.e.e.e
```

### Dynamické směrování
Jako protokol pro výměnu informací dynamického směrování použijeme RIP.
```
cisco(config)# router rip
cisco(config-router)# network a.b.c.d
cisco(config-router)# default-information originate
```
Příkaz network říká informaci, kudy se mají posílat informace i směrování, v tomto případě do sítě a.b.c.d. Příkaz default-information originate přidává informaci, že se má propagovat i výchozí směrovací záznam.
RIPng je modifikace protokolu RIP pro IPv6. Jeho konfigurace je podobná.
```
cisco(config)# ipv6 router rip name
cisco(config-rtr)# redistribute static
cisco(config-rtr)# redistribute connected
cisco(config-rtr)# exit
cisco(config)# interface FastEthernet 0/0
cisco(config-if)# ipv6 rip name enable
cisco(config-if)# ipv6 rip name default-information originate
```
Nastavení je třeba udělat pro všechna rozhraní, kterými se mají šířit informace. Příkaz redistribute určuje, jaké typy informací se mají šířit, kromě těch, které přijdou po síti. Např. static přeposílá statické záznamy, connected zase informace o přímo připojených sítích.
Bezestavová autokonfigurace
Automatická konfigurace se nevztahuje pouze na koncové stanice, lze ji využít i na směrovačích. Pro rychlé nastavení IPv6 adresy na směrovači stačí zadat příkaz:
```
cisco(config-if)# ipv6 address autoconfig
```

Tím se vytvoří link local adresa a je-li na síti i jiný směrovač, který vysílá RA, pak se nastaví i adresy a směrování podle RA.
RA se do sítě začne vysílat automaticky, jakmile nastavíme IPv6 adresu rozhraní. Pokud je toto nežádoucí jev, např. u rozhraní, které vede do Internetu, je nutné potlačit vysílání RA.
```
cisco(config-if)# ipv6 nd suppress-ra
```
Jestliže chceme změnit chování RA, můžeme je nastavit pomocí
```
cisco(config-if)# ipv6 nd ra-interval time
cisco(config-if)# ipv6 nd ra-lifetime time
```