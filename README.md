SMPP SS7 SIGTRAN
=========

Ukratko o SMPP, SS7 i SIGTRAN protokolima

SMPP (Short Message Peer-to-Peer)
------------

Short Message Peer-to-Peer (SMPP) je protokol za slanje i primanje sms poruka.
Jednostavan je za implementaciju i često se koristi za masovno (bulk) slanje sms poruka.
Poruke se šalju slanjem PDU (protocol data units) paketa u binarnom formatu a kod slanja PDU zaglavlje (header) je obavezno polje i sastoji se od:

* command_length - ukupna duljina PDU-a (uključujući command_length)
* command_id - operacija izvođenja (mogući id-evi su definirani specifikacijom smpp-a)
* command_status - sadrži informaciju o uspješnosti u odgovoru (kod zahtjeva status je uvijek 0)
* sequence_number - služi za praćenja zahtjeva i odgovora unutar jedne sesije


Uz header šalje se i sadržaj (body) poruke koji nije obavezan.

Najčešće se koristi verzija protokola 3.4, a dostupna je i verzija 3.3 i novija 5.0.
Sve poruke se šalju u binarnom "clear text" formatu, te je moguće implementirati SMPP preko SSL/TLS kanala ako ima potrebe. 

SS7 (Signalling System No. 7)
------------

SS7 je set signalnih protokola kojeg koristi većina telekom operatera a koristi se za uspostavu telefonskih poziva, slanje sms poruka...
Standardiziran je od strane American National Standards Institute-a (ANSI) i European Telecommunications Standards Institute-a (ETSI) i definiran po sljedećem modelu:

* MTP Level 1 (usporediv sa OSI modelom Layer 1 - Physical)
* MTP Level 2 (usporediv sa OSI modelom Layer 2 - Data link)
* MTP Level 3 i SCCP (usporedivi sa OSI modelom Layer 3 - Network)
* TUP, TCAP, ISUP... (usporedivi sa OSI modelom Layer 7 - Application)


Arhitektura SS7 protokola podijeljena je na 3 dijela:

1. Service Switching Point (SSP) - "telefonska centrala" koja šalje zahtjeve prema SCP-u
2. Signal Transfer Point (STP) - ruter zadužen za usmjeravanje podataka
3. Service Control Point (SCP) - poveznica na bazu podataka

Kao što se u računalnim mrežama koristi OSI model za određivanje pravila kako bi se podaci prenijeli preko komunkacijskih kanala, tako je i u telekomunikacijkoj mreži razvijen standard SS7.

SIGTRAN (SIGnaling TRANsport)
------------

SIGTRAN je nadogradnja SS7 protokola, tj. implementacija SS7 na IP protokolu (transportni sloj) ali umjesto TCP ili UDP protokola koristi Stream Control Transmission Protocol (SCTP).

SCTP je relativno novi protokol i sličan je TCP-u uz određene prednosti:

* Multihoming - odredište može imati više IP adresa (npr. od razčitih ISP-ova) što doprinosi redudanciji.
* Multistreaming - sctp podržava mutistreaming, dok TCP ne.
* Bolja zaštita od Man-In-The-Middle i DoS napada.

Bitno je naglasiti da kod implemetacije SIGTRAN-a nije potrebna specijalna oprema kao što je slučaj kod SS7, već se koristi standardna mrežna oprema.

Koristi se u novijim implementacijama kao što su 3G, 4G, 4G LTE...
