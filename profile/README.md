## PGPkeys EU

### SKS

SKS refers to both a software package (herein called [sks-keyserver](https://github.com/SKS-keyserver/sks-keyserver) for clarity), and the database synchronisation protocol that it speaks.
The sks-keyserver software is effectively end of life; the SKS protocol is not.
There are several other software packages that speak SKS, notably [Hockeypuck](https://github.com/hockeypuck/hockeypuck), and also [Peaks](https://github.com/r4yan2/peaks) (experimental).

### Synchronising and non-synchronising keyservers

The synchronising keyserver network is still operational, but has changed significantly in the last few years.
The main changes are:

1. the vast majority have been ported from sks-keyserver to hockeypuck, which has mitigated their stability issues
1. the sks-keyservers.net round-robin domain name has fallen into disuse due to legal uncertainty
1. many distributions (including debian and ubuntu) now use the non-synchronising keys.openpgp.org as their default

If you want to use a synchronising keyserver, you have to pick a specific provider from the list at https://spider.pgpkeys.eu.
Many people (including upstream gnupg) use https://keyserver.ubuntu.com because it has a good reputation for reliability, but it is not the only such choice.

In addition, there are several [non-synchronising keyservers](https://github.com/pgpkeys-eu/.github/wiki/Non-synchronising-keyservers) in common use, the best-known of which is https://keys.openpgp.org .
Unfortunately, there is currently no way to exhaustively search these keyservers for a given key without manually iterating through them.

All synchronising keyservers and most non-synchronising keyservers speak HKP, the de-facto standard keyserver lookup protocol supported by most OpenPGP clients.

### WKD and HKP

[Web Key Directory (WKD)](https://wiki.gnupg.org/WKD) is a modern key discovery protocol, however it is not a like-for-like replacement for HKP.
HKP keyservers and WKD are complementary protocols:

Feature                                               | HKP    | WKD
------------------------------------------------------|--------|--------
Key lookup by email userID                            | yes    | yes(1)
Key lookup by non-email userID                        | yes    | no
Key lookup by keyID/fingerprint                       | yes    | no
Key owner controls own key (self-sovereignty)         | no     | yes
Distribution of revocations                           | yes    | maybe(2)

1. WKD only works if the domain owner implements it.
2. Revocations are only distributed over WKD if the key owner specifically uploads them

### Background

The [SKS apocalypse](https://lists.gnu.org/archive/html/sks-devel/2018-05/msg00055.html) rendered the sks-keyserver software [effectively unusable](https://github.com/SKS-Keyserver/sks-keyserver/issues/57).
There are a few old systems still maintained as public-facing services but these are now in a distinct minority.

[Hockeypuck](https://hockeypuck.io) v2.1 and later mitigates the immediate problem by applying size limits to public keys.
This has been (at least initially) at the expense of a slightly broken recon algorithm.
In most cases this breakage has been absorbable, but a small number of operators have experienced runaway failure.
Work to fix this is part of our brief here.

### Links

* PGPkeys EU keyserver: https://pgpkeys.eu
* SKS network spider: https://spider.pgpkeys.eu
* Mastodon: https://infosec.exchange/@pgpkeys
