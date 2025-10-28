**def**: Wireshark is an [[open-source]], cross-platform [[network packet analyser]] tool capable of [sniffing] and [[investigating]] live [[traffic]] and inspecting packet captures ([[pcap]]).
- coloring [[packets]] ; view -> coloring rules
- mrege PCAPS : file -> merge
- **very important :** statistics -> [[capture]] file properties
- go -> go to packet
- edit -> find packet
	- string/ regex
	- search fiels 
- mark packet : edit -> mark (marked shown in black)
- comments : mouse R click -> packet comment |OR| edit -> packet comment
- export (**take something out** of a system so you can use it **somewhere else**.): file -> export specified packet (as .pcap or .pcapng) / export object (like files downloaded in traffic) / export packet dissection(as Plain Text, JSON, etc.)
- time :  view -> time display format
- expert info : analyse -> expert information
	![[Screenshot_20250707_163037.png]]

| group          | **Info**                   |
| -------------- | -------------------------- |
| **Checksum**   | Checksum errors            |
| **Comment**    | Packet comment detection   |
| **Deprecated** | Deprecated protocol usage  |
| **Malformed**  | Malformed packet detection |
- Apply as Filter : analyse -> apply as filter
- Conversation Filter : Analyse -> Conversation Filter
- Colourise [[Conversation]] : View -> Colourise Conversation -> Reset Colourisation
- Prepare as Filter : similar to apply as filter
