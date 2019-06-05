# Proposed Data Encoding Table

Mappings should be [datatype][name][separator][data].

( Separator is proposed to be 0xFF but others could be used )

Constant length 2+-byte data field | Proposed Data Standard                 | Separator | Description
-----------------------------------|----------------------------------------|-----------|-------------
00                                 | Private Usage                          | 0xFF      | The data associated with the name has no explicitly stated purpose. The data SHOULD NOT be used to verify any other consensus-approved data standard.
01                                 | Bitcoin Address                        | 0xFF      | The data associated with the name SHOULD BE used to TRUST that the Bitcoin address is associated to the given name.
02                                 | Lightning Node Public Key              | 0xFF      | The data associated with the name SHOULD BE used to TRUST an advertised ALIAS of a Lightning node.
03                                 | GPG Public Key                         | 0xFF      | The data associated with the name SHOULD BE used to TRUST a GPG Public Key
04                                 | Domain-validated Certificate           | 0xFF      | The data SHOULD BE a domain certificate for the specified name (ex: example.com)
05                                 | DNS mapping                            | 0xFF      | The data SHOULD BE a valid IP address.
06                                 | Tor mapping                            | 0xFF      | The data SHOULD BE an Tor onion address.
07                                 | Software Signing Key                   | 0xFF      | The data SHOULD BE a public key to verify signed software packages.
08-FF                              | Future use decided upon via consensus. | 0xFF      | Future use
