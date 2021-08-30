# srtp-decrypt for Windows (Win64)
srtp-decrypt is a tool that deciphers SRTP packets contained in a network capture. It needs the Master Key exchanged by other means to do its job.
Deciphered RTP is dumped in such a way that output can be fed to text2pcap, to recreate a deciphered capture.

dependencies (already precompiled libs)
============
- LibSrtp
- WinPcap

caveats
=======
- Isolating a single RTP flow from a network capture is a hard job, too hard to be done in this tool. Hence, srtp-decrypt expects to process a single RTP flow.
- Network capture shall not contain ICMP, ARP or reverse RTP flow for example, as those packets will not be deciphered correctly by the tool.
- Moreover, RTP offset in frames is expected to be constant, by default 42, but can be set to 46 in case of 802.1q tagging.

an example of use:
=======
./srtp-decrypt -s AES_CM_128_HMAC_SHA1_80 -b ZfSkISbtsGTKws4Gi0txMeLhgrAjlU5uQCuvZgLv < ./enc_stream.pcap | text2pcap -t "%M:%S." -u 10000,10000 - - > ./dec_stream.pcap
