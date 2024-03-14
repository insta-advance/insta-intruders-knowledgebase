# Access control systems

## Cards

Many NFC cards have vulnerabilities, allowing them to be cloned or manipulated. Notably the algorithm used in Mifare Classic has been cracked, allowing Mifare Classic cards to be cloned using a specific tool, such as a Flipper Zero or a Proxmark 3.

[More information about RFID hacking](https://book.hacktricks.xyz/todo/radio-hacking/pentesting-rfid)

### NFC

#### Mifare Classic

Many Mifare Classic cards use default keys to protect their sectors, which are included in the Flipper Zero's dictionary for example. If using the Flipper Zero, reading a card will automatically try these keys against the card.

If the key used by a sector on the card is not in the dictionary, the Flipper will not be able to read it just by reading the card. Then the "Detect Reader" mode in the Flipper can be used to collect keys from a Mifare Classic reader by emulating the card using the Mfkey32 attack. After the keys are collected into the dictionary, the card can be cracked.

### RFID

Low-frequency RFID tags are generally quite insecure. They do not have any cryptography in them, and just broadcast their ID, which can unlock the door. These can be cloned with the Flipper Zero for example.

## Readers

The readers of access control cards can be attacked. Readers need to have a way of communicating to the door that it needs to be opened. Some cheap systems work so that the reader just sends a signal to a wire connected to the door lock, which makes it easy to open the door lock and connect some pins to open the door.

More sophisticated readers typically have a protocol which they use to send the card data to a separate unit inside, which validates that the card should have access through the door. Typically used protocols are Wiegand and OSDP.

### Wiegand

Wiegand has no encryption, making it vulnerable to sniffing. An attacker can install a device to sniff card data passing from the reader to the system inside, so that valid card data can be collected and reused in an attack. 

### OSDP

OSDP has encryption, but it is fairly insecure. 

[Good DEF CON talk about OSDP](https://www.youtube.com/watch?v=zNpM_l5l0sE)

