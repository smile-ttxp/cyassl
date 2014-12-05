# Notes - Please read 

## Note 1
```
CyaSSL now needs all examples and tests to be run from the CyaSSL home
directory.  This is because it finds certs and keys from ./certs/.  Trying to
maintain the ability to run each program from its own directory, the testsuite
directory, the main directory (for make check/test), and for the various
different project layouts (with or without config) was becoming harder and 
harder.  Now to run testsuite just do:

./testsuite/testsuite

or 

make check    (when using autoconf)

On *nix or Windows the examples and testsuite will check to see if the current
directory is the source directory and if so, attempt to change to the CyaSSL
home directory.  This should work in most setup cases, if not, just follow the
beginning of the note and specify the full path.
```

## Note 2
```
CyaSSL takes a different approach to certificate verification than OpenSSL does.
The default policy for the client is to verify the server, this means that if
you don't load CAs to verify the server you'll get a connect error, no signer
error to confirm failure (-188).  If you want to mimic OpenSSL behavior of
having SSL_connect succeed even if verifying the server fails and reducing
security you can do this by calling:

SSL_CTX_set_verify(ctx, SSL_VERIFY_NONE, 0);

before calling SSL_new();  Though it's not recommended.
```


# CyaSSL Release 3.3.0 (12/05/2014)

- Countermeasuers for Handshake message duplicates, CHANGE CIPHER without
  FINISHED, and fast forward attempts.  Thanks to Karthikeyan Bhargavan from
  the Prosecco team at INRIA Paris-Rocquencourt for the report.
- FIPS version submitted
- Removes SSLv2 Client Hello processing, can be enabled with OLD_HELLO_ALLOWED
- User can set mimimum downgrade version with CyaSSL_SetMinVersion()
- Small stack improvements at TLS/SSL layer
- TLS Master Secret generation and Key Expansion are now exposed
- Adds client side Secure Renegotiation, * not recommended *
- Client side session ticket support, not fully tested with Secure Renegotiation
- Allows up to 4096bit DHE at TLS Key Exchange layer
- Handles non standard SessionID sizes in Hello Messages
- PicoTCP Support
- Sniffer now supports SNI Virtual Hosts
- Sniffer now handles non HTTPS protocols using STARTTLS
- Sniffer can now parse records with multiple messages
- TI-RTOS updates
- Fix for ColdFire optimized fp_digit read only in explicit 32bit case
- ADH Cipher Suite ADH-AES128-SHA for EAP-FAST

The CyaSSL manual is available at:
http://www.wolfssl.com/documentation/CyaSSL-Manual.pdf.  For build instructions
and comments about the new features please check the manual.


# CyaSSL Release 3.2.0 (09/10/2014)

#### Release 3.2.0 CyaSSL has bug fixes and new features including:

- ChaCha20 and Poly1305 crypto and suites
- Small stack improvements for OCSP, CRL, TLS, DTLS
- NTRU Encrypt and Decrypt benchmarks
- Updated Visual Studio project files
- Updated Keil MDK5 project files
- Fix for DTLS sequence numbers with GCM/CCM
- Updated HashDRBG with more secure struct declaration
- TI-RTOS support and example Code Composer Studio project files
- Ability to get enabled cipher suites, CyaSSL_get_ciphers()
- AES-GCM/CCM/Direct support for Freescale mmCAU and CAU
- Sniffer improvement checking for decrypt key setup
- Support for raw ECC key import
- Ability to convert ecc_key to DER, EccKeyToDer()
- Security fix for RSA Padding check vulnerability reported by Intel Security
  Advanced Threat Research team

The CyaSSL manual is available at:
http://www.wolfssl.com/documentation/CyaSSL-Manual.pdf.  For build instructions
and comments about the new features please check the manual.


# CyaSSL Release 3.1.0 (07/14/2014)

#### Release 3.1.0 CyaSSL has bug fixes and new features including:

- Fix for older versions of icc without 128-bit type
- Intel ASM syntax for AES-NI
- Updated NTRU support, keygen benchmark
- FIPS check for minimum required HMAC key length
- Small stack (--enable-smallstack) improvements for PKCS#7, ASN
- TLS extension support for DTLS
- Default I/O callbacks external to user
- Updated example client with bad clock test
- Ability to set optional ECC context info
- Ability to enable/disable DH separate from opensslextra
- Additional test key/cert buffers for CA and server
- Updated example certificates

The CyaSSL manual is available at:
http://www.yassl.com/documentation/CyaSSL-Manual.pdf.  For build instructions
and comments about the new features please check the manual.


# CyaSSL Release 3.0.2 (05/30/2014)

#### Release 3.0.2 CyaSSL has bug fixes and new features including:

- Added the following cipher suites:
  * TLS_PSK_WITH_AES_128_GCM_SHA256
  * TLS_PSK_WITH_AES_256_GCM_SHA384
  * TLS_PSK_WITH_AES_256_CBC_SHA384
  * TLS_PSK_WITH_NULL_SHA384
  * TLS_DHE_PSK_WITH_AES_128_GCM_SHA256
  * TLS_DHE_PSK_WITH_AES_256_GCM_SHA384
  * TLS_DHE_PSK_WITH_AES_128_CBC_SHA256
  * TLS_DHE_PSK_WITH_AES_256_CBC_SHA384
  * TLS_DHE_PSK_WITH_NULL_SHA256
  * TLS_DHE_PSK_WITH_NULL_SHA384
  * TLS_DHE_PSK_WITH_AES_128_CCM
  * TLS_DHE_PSK_WITH_AES_256_CCM
- Added AES-NI support for Microsoft Visual Studio builds.
- Changed small stack build to be disabled by default.
- Updated the Hash DRBG and provided a configure option to enable.

The CyaSSL manual is available at:
http://www.yassl.com/documentation/CyaSSL-Manual.pdf.  For build instructions
and comments about the new features please check the manual.


# CyaSSL Release 3.0.0 (04/29/2014)

#### Release 3.0.0 CyaSSL has bug fixes and new features including:

- FIPS release candidate
- X.509 improvements that address items reported by Suman Jana with security
  researchers at UT Austin and UC Davis
- Small stack size improvements, --enable-smallstack. Offloads large local
  variables to the heap. (Note this is not complete.)
- Updated AES-CCM-8 cipher suites to use approved suite numbers.

The CyaSSL manual is available at:
http://www.yassl.com/documentation/CyaSSL-Manual.pdf.  For build instructions
and comments about the new features please check the manual.


# CyaSSL Release 2.9.4 (04/09/2014)

#### Release 2.9.4 CyaSSL has bug fixes and new features including:

- Security fixes that address items reported by Ivan Fratric of the Google
  Security Team
- X.509 Unknown critical extensions treated as errors, report by Suman Jana with
  security researchers at UT Austin and UC Davis
- Sniffer fixes for corrupted packet length and Jumbo frames
- ARM thumb mode assembly fixes
- Xcode 5.1 support including new clang
- PIC32 MZ hardware support
- CyaSSL Object has enough room to read the Record Header now w/o allocs
- FIPS wrappers for AES, 3DES, SHA1, SHA256, SHA384, HMAC, and RSA.
- A sample I/O pool is demonstrated with --enable-iopool to overtake memory
  handling and reduce memory fragmentation on I/O large sizes

The CyaSSL manual is available at:
http://www.yassl.com/documentation/CyaSSL-Manual.pdf.  For build instructions 
and comments about the new features please check the manual.


# CyaSSL Release 2.9.0 (02/07/2014)

#### Release 2.9.0 CyaSSL has bug fixes and new features including:
- Freescale Kinetis RNGB support
- Freescale Kinetis mmCAU support
- TLS Hello extensions
  - ECC
  - Secure Renegotiation (null) 
  - Truncated HMAC
- SCEP support
  - PKCS #7 Enveloped data and signed data
  - PKCS #10 Certificate Signing Request generation
- DTLS sliding window
- OCSP Improvements
  - API change to integrate into Certificate Manager
  - IPv4/IPv6 agnostic
  - example client/server support for OCSP
  - OCSP nonces are optional
- GMAC hashing
- Windows build additions
- Windows CYGWIN build fixes
- Updated test certificates
- Microchip MPLAB Harmony support
- Update autoconf scripts
- Additional X.509 inspection functions
- ECC encrypt/decrypt primitives
- ECC Certificate generation

The Freescale Kinetis K53 RNGB documentation can be found in Chapter 33 of the
K53 Sub-Family Reference Manual:
http://cache.freescale.com/files/32bit/doc/ref_manual/K53P144M100SF2RM.pdf

Freescale Kinetis K60 mmCAU (AES, DES, 3DES, MD5, SHA, SHA256) documentation
can be found in the "ColdFire/ColdFire+ CAU and Kinetis mmCAU Software Library
User Guide":
http://cache.freescale.com/files/32bit/doc/user_guide/CAUAPIUG.pdf


# CyaSSL Release 2.8.0 (8/30/2013)

#### Release 2.8.0 CyaSSL has bug fixes and new features including:
- AES-GCM and AES-CCM use AES-NI
- NetX default IO callback handlers
- IPv6 fixes for DTLS Hello Cookies
- The ability to unload Certs/Keys after the handshake, CyaSSL_UnloadCertsKeys()
- SEP certificate extensions
- Callback getters for easier resource freeing
- External CYASSL_MAX_ERROR_SZ for correct error buffer sizing
- MacEncrypt and DecryptVerify Callbacks for User Atomic Record Layer Processing
- Public Key Callbacks for ECC and RSA
- Client now sends blank cert upon request if doesn't have one with TLS <= 1.2


The CyaSSL manual is available at:
http://www.yassl.com/documentation/CyaSSL-Manual.pdf.  For build instructions 
and comments about the new features please check the manual.


# CyaSSL Release 2.7.0 (6/17/2013)

#### Release 2.7.0 CyaSSL has bug fixes and new features including:
- SNI support for client and server
- KEIL MDK-ARM projects
- Wildcard check to domain name match, and Subject altnames are checked too
- Better error messages for certificate verification errors
- Ability to discard session during handshake verify
- More consistent error returns across all APIs
- Ability to unload CAs at the CTX or CertManager level
- Authority subject id support for Certificate matching
- Persistent session cache functionality
- Persistent CA cache functionality
- Client session table lookups to push serverID table to library level
- Camellia support to sniffer
- User controllable settings for DTLS timeout values
- Sniffer fixes for caching long lived sessions
- DTLS reliability enhancements for the handshake
- Better ThreadX support

When compiling with Mingw, libtool may give the following warning due to
path conversion errors:
 
```
libtool: link: Could not determine host file name corresponding to **
libtool: link: Continuing, but uninstalled executables may not work.
```

If so, examples and testsuite will have problems when run, showing an
error while loading shared libraries. To resolve, please run "make install".

The CyaSSL manual is available at:
http://www.yassl.com/documentation/CyaSSL-Manual.pdf.  For build instructions 
and comments about the new features please check the manual.


# CyaSSL Release 2.6.0 (04/15/2013)

#### Release 2.6.0 CyaSSL has bug fixes and new features including:
- DTLS 1.2 support including AEAD ciphers
- SHA-3 finalist Blake2 support, it's fast and uses little resources
- SHA-384 cipher suites including ECC ones
- HMAC now supports SHA-512
- Track memory use for example client/server with -t option
- Better IPv6 examples with --enable-ipv6, before if ipv6 examples/tests were
  turned on, localhost only was used.  Now link-local (with scope ids) and ipv6
  hosts can be used as well.
- Xcode v4.6 project for iOS v6.1 update
- settings.h is now checked in all *.c files for true one file setting detection
- Better alignment at SSL layer for hardware crypto alignment needs
    * Note, SSL itself isn't friendly to alignment with 5 byte TLS headers and
      13 bytes DTLS headers, but every effort is now made to align with the
      CYASSL_GENERAL_ALIGNMENT flag which sets desired alignment requirement
- NO_64BIT flag to turn off 64bit data type accumulators in public key code
    * Note, some systems are faster with 32bit accumulators 
- --enable-stacksize for example client/server stack use
    * Note, modern desktop Operating Systems may add bytes to each stack frame
- Updated compression/decompression with direct crypto access
- All ./configure options are now lowercase only for consistency
- ./configure builds default to fastmath option
    * Note, if on ia32 and building in shared mode this may produce a problem
      with a missing register being available because of PIC, there are at least
      5 solutions to this:
      1) --disable-fastmath , don't use fastmath
      2) --disable-shared, don't build a shared library
      3) C_EXTRA_FLAGS=-DTFM_NO_ASM , turn off assembly use
      4) use clang, it just seems to work
      5) play around with no PIC options to force all registers being open
- Many new ./configure switches for option enable/disable for example
    * rsa
    * dh
    * dsa
    * md5
    * sha 
    * arc4
    * null    (allow NULL ciphers)
    * oldtls  (only use TLS 1.2)
    * asn     (no certs or public keys allowed)
- ./configure generates cyassl/options.h which allows a header the user can 
  include in their app to make sure the same options are set at the app and
  CyaSSL level.
- autoconf no longer needs serial-tests which lowers version requirements of
  automake to 1.11 and autoconf to 2.63

The CyaSSL manual is available at:
http://www.yassl.com/documentation/CyaSSL-Manual.pdf.  For build instructions 
and comments about the new features please check the manual.



# CyaSSL Release 2.5.0 (02/04/2013)

#### Release 2.5.0 CyaSSL has bug fixes and new features including:
- Fix for TLS CBC padding timing attack identified by Nadhem Alfardan and
  Kenny Paterson: http://www.isg.rhul.ac.uk/tls/
- Microchip PIC32 (MIPS16, MIPS32) support
- Microchip MPLAB X example projects for PIC32 Ethernet Starter Kit
- Updated CTaoCrypt benchmark app for embedded systems
- 1024-bit test certs/keys and cert/key buffers
- AES-CCM-8 crypto and cipher suites
- Camellia crypto and cipher suites
- Bumped minimum autoconf version to 2.65, automake version to 1.12
- Addition of OCSP callbacks
- STM32F2 support with hardware crypto and RNG 
- Cavium NITROX support

CTaoCrypt now has support for the Microchip PIC32 and has been tested with
the Microchip PIC32 Ethernet Starter Kit, the XC32 compiler and
MPLAB X IDE in both MIPS16 and MIPS32 instruction set modes. See the README
located under the <cyassl_root>/mplabx directory for more details.

To add Cavium NITROX support do:

./configure --with-cavium=/home/user/cavium/software

pointing to your licensed cavium/software directory.  Since Cavium doesn't
build a library we pull in the cavium_common.o file which gives a libtool 
warning about the portability of this.  Also, if you're using the github source
tree you'll need to remove the -Wredundant-decls warning from the generated
Makefile because the cavium headers don't conform to this warning.  Currently
CyaSSL supports Cavium RNG, AES, 3DES, RC4, HMAC, and RSA directly at the crypto
layer.  Support at the SSL level is partial and currently just does AES, 3DES,
and RC4.  RSA and HMAC are slower until the Cavium calls can be utilized in non
blocking mode.  The example client turns on cavium support as does the crypto
test and benchmark.  Please see the HAVE_CAVIUM define.

CyaSSL is able to use the STM32F2 hardware-based cryptography and random number
generator through the STM32F2 Standard Peripheral Library. For necessary
defines, see the CYASSL_STM32F2 define in settings.h. Documentation for the
STM32F2 Standard Peripheral Library can be found in the following document: 
http://www.st.com/internet/com/TECHNICAL_RESOURCES/TECHNICAL_LITERATURE/USER_MANUAL/DM00023896.pdf

The CyaSSL manual is available at:
http://www.yassl.com/documentation/CyaSSL-Manual.pdf.  For build instructions 
and comments about the new features please check the manual.



# CyaSSL Release 2.4.6 (12/20/2012)

#### Release 2.4.6 CyaSSL has bug fixes and a few new features including:
- ECC into main version
- Lean PSK build (reduced code size, RAM usage, and stack usage)
- FreeBSD CRL monitor support
- CyaSSL_peek()
- CyaSSL_send() and CyaSSL_recv() for I/O flag setting
- CodeWarrior Support
- MQX Support
- Freescale Kinetis support including Hardware RNG
- autoconf builds use jobserver
- cyassl-config
- Sniffer memory reductions

Thanks to Brian Aker for the improved autoconf system, make rpm, cyassl-config,
warning system, and general good ideas for improving CyaSSL!

The Freescale Kinetis K70 RNGA documentation can be found in Chapter 37 of the
K70 Sub-Family Reference Manual:
http://cache.freescale.com/files/microcontrollers/doc/ref_manual/K70P256M150SF3RM.pdf

The CyaSSL manual is available at:
http://www.yassl.com/documentation/CyaSSL-Manual.pdf.  For build instructions 
and comments about the new features please check the manual.


# CyaSSL Release 2.4.0 (10/10/2012)

#### Release 2.4.0 CyaSSL has bug fixes and a few new features including:
- DTLS reliability
- Reduced memory usage after handshake
- Updated build process

The CyaSSL manual is available at:
http://www.yassl.com/documentation/CyaSSL-Manual.pdf.  For build instructions 
and comments about the new features please check the manual.



# CyaSSL Release 2.3.0 (8/10/2012)

#### Release 2.3.0 CyaSSL has bug fixes and a few new features including:
- AES-GCM crypto and cipher suites
- make test cipher suite checks
- Subject AltName processing
- Command line support for client/server examples
- Sniffer SessionTicket support
- SHA-384 cipher suites
- Verify cipher suite validity when user overrides
- CRL dir monitoring
- DTLS Cookie support, reliability coming soon

The CyaSSL manual is available at:
http://www.yassl.com/documentation/CyaSSL-Manual.pdf.  For build instructions 
and comments about the new features please check the manual.



# CyaSSL Release 2.2.0 (5/18/2012)

#### Release 2.2.0 CyaSSL has bug fixes and a few new features including:
- Initial CRL support (--enable-crl)
- Initial OCSP support (--enable-ocsp)
- Add static ECDH suites
- SHA-384 support
- ECC client certificate support
- Add medium session cache size (1055 sessions) 
- Updated unit tests
- Protection against mutex reinitialization


The CyaSSL manual is available at:
http://www.yassl.com/documentation/CyaSSL-Manual.pdf.  For build instructions 
and comments about the new features please check the manual.



# CyaSSL Release 2.0.8 (2/24/2012)

#### Release 2.0.8 CyaSSL has bug fixes and a few new features including:
- A fix for malicious certificates pointed out by Remi Gacogne (thanks)
  resulting in NULL pointer use.
- Respond to renegotiation attempt with no_renegoatation alert
- Add basic path support for load_verify_locations()
- Add set Temp EC-DHE key size
- Extra checks on rsa test when porting into


The CyaSSL manual is available at:
http://www.yassl.com/documentation/CyaSSL-Manual.pdf.  For build instructions 
and comments about the new features please check the manual.



# CyaSSL Release 2.0.6 (1/27/2012)

#### Release 2.0.6 CyaSSL has bug fixes and a few new features including:
- Fixes for CA basis constraint check
- CTX reference counting
- Initial unit test additions
- Lean and Mean Windows fix
- ECC benchmarking
- SSMTP build support
- Ability to group handshake messages with set_group_messages(ctx/ssl)
- CA cache addition callback
- Export Base64_Encode for general use

The CyaSSL manual is available at:
http://www.yassl.com/documentation/CyaSSL-Manual.pdf.  For build instructions 
and comments about the new features please check the manual.



# CyaSSL Release 2.0.2 (12/05/2011)

#### Release 2.0.2 CyaSSL has bug fixes and a few new features including:
- CTaoCrypt Runtime library detection settings when directly using the crypto
  library
- Default certificate generation now uses SHAwRSA and adds SHA256wRSA generation
- All test certificates now use 2048bit and SHA-1 for better modern browser
  support
- Direct AES block access and AES-CTR (counter) mode
- Microchip pic32 support

The CyaSSL manual is available at:
http://www.yassl.com/documentation/CyaSSL-Manual.pdf.  For build instructions 
and comments about the new features please check the manual.



# CyaSSL Release 2.0.0rc3 (9/28/2011)

#### Release 2.0.0rc3 for CyaSSL has bug fixes and a few new features including:
- updated autoconf support
- better make install and uninstall  (uses system directories)
- make test / make check
- CyaSSL headers now in <cyassl/*.h>
- CTaocrypt headers now in <cyassl/ctaocrypt/*.h>
- OpenSSL compatibility headers now in <cyassl/openssl/*.h>
- examples and tests all run from home directory so can use certs in ./certs
        (see note 1)

So previous applications that used the OpenSSL compatibility header
<openssl/ssl.h> now need to include <cyassl/openssl/ssl.h> instead, no other
changes are required.

Special Thanks to Brian Aker for his autoconf, install, and header patches.

The CyaSSL manual is available at:
http://www.yassl.com/documentation/CyaSSL-Manual.pdf.  For build instructions 
and comments about the new features please check the manual.

# CyaSSL Release 2.0.0rc2 (6/6/2011)

#### Release 2.0.0rc2 for CyaSSL has bug fixes and a few new features including:
- bug fixes (Alerts, DTLS with DHE)
- FreeRTOS support
- lwIP support
- Wshadow warnings removed
- asn public header
- CTaoCrypt public headers now all have ctc_ prefix (the manual is still being
        updated to reflect this change)
- and more.

This is the 2nd and perhaps final release candidate for version 2.
Please send any comments or questions to support@yassl.com.

The CyaSSL manual is available at:
http://www.yassl.com/documentation/CyaSSL-Manual.pdf.  For build instructions 
and comments about the new features please check the manual.

# CyaSSL Release 2.0.0rc1 (5/2/2011)

#### Release 2.0.0rc1 for CyaSSL has many new features including:
- bug fixes
- SHA-256 cipher suites 
- Root Certificate Verification (instead of needing all certs in the chain) 
- PKCS #8 private key encryption (supports PKCS #5 v1-v2 and PKCS #12) 
- Serial number retrieval for x509 
- PBKDF2 and PKCS #12 PBKDF 
- UID parsing for x509 
- SHA-256 certificate signatures 
- Client and server can send chains (SSL_CTX_use_certificate_chain_file) 
- CA loading can now parse multiple certificates per file
- Dynamic memory runtime hooks
- Runtime hooks for logging
- EDH on server side
- More informative error codes
- More informative logging messages
- Version downgrade more robust (use SSL_v23*)
- Shared build only by default through ./configure
- Compiler visibility is now used, internal functions not polluting namespace
- Single Makefile, no recursion, for faster and simpler building
- Turn on all warnings possible build option, warning fixes
- and more.

Because of all the new features and the multiple OS, compiler, feature-set
options that CyaSSL allows, there may be some configuration fixes needed.
Please send any comments or questions to support@yassl.com.

The CyaSSL manual is available at:
http://www.yassl.com/documentation/CyaSSL-Manual.pdf.  For build instructions 
and comments about the new features please check the manual.

# CyaSSL Release 1.9.0 (3/2/2011)

Release 1.9.0 for CyaSSL adds bug fixes, improved TLSv1.2 through testing and
better hash/sig algo ids, --enable-webServer for the yaSSL embedded web server,
improper AES key setup detection, user cert verify callback improvements, and
more.

The CyaSSL manual offering is included in the doc/ directory.  For build
instructions and comments about the new features please check the manual.

Please send any comments or questions to support@yassl.com.

# CyaSSL Release 1.8.0 (12/23/2010)

Release 1.8.0 for CyaSSL adds bug fixes, x509 v3 CA signed certificate
generation, a C standard library abstraction layer, lower memory use, increased
portability through the os_settings.h file, and the ability to use NTRU cipher
suites when used in conjunction with an NTRU license and library.

The initial CyaSSL manual offering is included in the doc/ directory.  For
build instructions and comments about the new features please check the manual.

Please send any comments or questions to support@yassl.com.

Happy Holidays.
 

# CyaSSL Release 1.6.5 (9/9/2010)

Release 1.6.5 for CyaSSL adds bug fixes and x509 v3 self signed certificate
generation.
 
For general build instructions see doc/Building_CyaSSL.pdf.

To enable certificate generation support add this option to ./configure
./configure --enable-certgen

An example is included in ctaocrypt/test/test.c and documentation is provided
in doc/CyaSSL_Extensions_Reference.pdf item 11.

# CyaSSL Release 1.6.0 (8/27/2010)

Release 1.6.0 for CyaSSL adds bug fixes, RIPEMD-160, SHA-512, and RSA key
generation.
 
For general build instructions see doc/Building_CyaSSL.pdf.

To add RIPEMD-160 support add this option to ./configure
./configure --enable-ripemd

To add SHA-512 support add this option to ./configure
./configure --enable-sha512

To add RSA key generation support add this option to ./configure
./configure --enable-keygen

Please see ctaocrypt/test/test.c for examples and usage.

For Windows, RIPEMD-160 and SHA-512 are enabled by default but key generation is
off by default.  To turn key generation on add the define CYASSL_KEY_GEN to
CyaSSL.


# CyaSSL Release 1.5.6 (7/28/2010)

Release 1.5.6 for CyaSSL adds bug fixes, compatibility for our JSSE provider,
and a fix for GCC builds on some systems.
 
For general build instructions see doc/Building_CyaSSL.pdf.

To add AES-NI support add this option to ./configure
./configure --enable-aesni

You'll need GCC 4.4.3 or later to make use of the assembly.

# CyaSSL Release 1.5.4 (7/7/2010)

Release 1.5.4 for CyaSSL adds bug fixes, support for AES-NI, SHA1 speed 
improvements from loop unrolling, and support for the Mongoose Web Server.
 
For general build instructions see doc/Building_CyaSSL.pdf.

To add AES-NI support add this option to ./configure
./configure --enable-aesni

You'll need GCC 4.4.3 or later to make use of the assembly.

# CyaSSL Release 1.5.0 (5/11/2010)

Release 1.5.0 for CyaSSL adds bug fixes, GoAhead WebServer support, sniffer
support, and initial swig interface support.

For general build instructions see doc/Building_CyaSSL.pdf.

To add support for GoAhead WebServer either --enable-opensslExtra or if you
don't want all the features of opensslExtra you can just define GOAHEAD_WS
instead.  GOAHEAD_WS can be added to ./configure with CFLAGS=-DGOAHEAD_WS or
you can define it yourself.

To look at the sniffer support please see the sniffertest app in
sslSniffer/sslSnifferTest.  Build with --enable-sniffer on *nix or use the
vcproj files on windows.  You'll need to have pcap installed on *nix and
WinPcap on windows.

A swig interface file is now located in the swig directory for using Python,
Java, Perl, and others with CyaSSL.  This is initial support and experimental,
please send questions or comments to support@yassl.com.

When doing load testing with CyaSSL, on the echoserver example say, the client
machine may run out of tcp ephemeral ports, they will end up in the TIME_WAIT
queue, and can't be reused by default.  There are generally two ways to fix
this. 

1. Reduce the length sockets remain on the TIME_WAIT queue OR
2. Allow items on the TIME_WAIT queue to be reused.


To reduce the TIME_WAIT length in OS X to 3 seconds (3000 milliseconds)

`sudo sysctl -w net.inet.tcp.msl=3000`

In Linux

`sudo sysctl -w net.ipv4.tcp_tw_reuse=1`

allows reuse of sockets in TIME_WAIT

`sudo sysctl -w net.ipv4.tcp_tw_recycle=1`

works but seems to remove sockets from  TIME_WAIT entirely?

`sudo sysctl -w net.ipv4.tcp_fin_timeout=1`

doen't control TIME_WAIT, it controls FIN_WAIT(2) contrary to some posts


# CyaSSL Release 1.4.0 (2/18/2010)

Release 1.3.0 for CyaSSL adds bug fixes, better multi TLS/SSL version support
through SSLv23_server_method(), and improved documentation in the doc/ folder.

For general build instructions doc/Building_CyaSSL.pdf.

# CyaSSL Release 1.3.0 (1/21/2010)

Release 1.3.0 for CyaSSL adds bug fixes, a potential security problem fix,
better porting support, removal of assert()s, and a complete THREADX port.

For general build instructions see rc1 below.

# CyaSSL Release 1.2.0 (11/2/2009)

Release 1.2.0 for CyaSSL adds bug fixes and session negotiation if first use is
read or write.

For general build instructions see rc1 below.

# CyaSSL Release 1.1.0 (9/2/2009)

Release 1.1.0 for CyaSSL adds bug fixes, a check against malicious session
cache use, support for lighttpd, and TLS 1.2.

To get TLS 1.2 support please use the client and server functions:

```c
SSL_METHOD *TLSv1_2_server_method(void);
SSL_METHOD *TLSv1_2_client_method(void);
```

CyaSSL was tested against lighttpd 1.4.23.  To build CyaSSL for use with 
lighttpd use the following commands from the CyaSSL install dir <CyaSSLDir>:

```
./configure --disable-shared --enable-opensslExtra --enable-fastmath --without-zlib

make
make openssl-links
```

Then to build lighttpd with CyaSSL use the following commands from the
lighttpd install dir:

```
./configure --with-openssl --with-openssl-includes=<CyaSSLDir>/include --with-openssl-libs=<CyaSSLDir>/lib LDFLAGS=-lm

make
```

On some systems you may get a linker error about a duplicate symbol for
MD5_Init or other MD5 calls.  This seems to be caused by the lighttpd src file
md5.c, which defines MD5_Init(), and is included in liblightcomp_la-md5.o.
When liblightcomp is linked with the SSL_LIBs the linker may complain about
the duplicate symbol.  This can be fixed by editing the lighttpd src file md5.c
and adding this line to the beginning of the file:

\#if 0

and this line to the end of the file

\#endif

Then from the lighttpd src dir do a:

```
make clean
make
```

If you get link errors about undefined symbols more than likely the actual
OpenSSL libraries are found by the linker before the CyaSSL openssl-links that
point to the CyaSSL library, causing the linker confusion.  This can be fixed
by editing the Makefile in the lighttpd src directory and changing the line:

`SSL_LIB = -lssl -lcrypto`

to

`SSL_LIB = -lcyassl`

Then from the lighttpd src dir do a:

```
make clean
make
```

This should remove any confusion the linker may be having with missing symbols.

For any questions or concerns please contact support@yassl.com .

For general build instructions see rc1 below.

# CyaSSL Release 1.0.6 (8/03/2009)

Release 1.0.6 for CyaSSL adds bug fixes, an improved session cache, and faster
math with a huge code option.

The session cache now defaults to a client mode, also good for embedded servers.
For servers not under heavy load (less than 200 new sessions per minute), define
BIG_SESSION_CACHE.  If the server will be under heavy load, define
HUGE_SESSION_CACHE.

There is now a fasthugemath option for configure.  This enables fastmath plus
even faster math by greatly increasing the code size of the math library. Use
the benchmark utility to compare public key operations.


For general build instructions see rc1 below.

# CyaSSL Release 1.0.3 (5/10/2009)

Release 1.0.3 for CyaSSL adds bug fixes and add increased support for OpenSSL
compatibility when building other applications.

Release 1.0.3 includes an alpha release of DTLS for both client and servers.
This is only for testing purposes at this time.  Rebroadcast and reordering
aren't fully implemented at this time but will be for the next release.

For general build instructions see rc1 below.

# CyaSSL Release 1.0.2 (4/3/2009)

Release 1.0.2 for CyaSSL adds bug fixes for a couple I/O issues.  Some systems
will send a SIGPIPE on socket recv() at any time and this should be handled by
the application by turning off SIGPIPE through setsockopt() or returning from
the handler.

Release 1.0.2 includes an alpha release of DTLS for both client and servers.
This is only for testing purposes at this time.  Rebroadcast and reordering
aren't fully implemented at this time but will be for the next release.

For general build instructions see rc1 below.

## CyaSSL Release Candidiate 3 rc3-1.0.0 (2/25/2009)


Release Candidate 3 for CyaSSL 1.0.0 adds bug fixes and adds a project file for
iPhone development with Xcode.  cyassl-iphone.xcodeproj is located in the root
directory.  This release also includes a fix for supporting other
implementations that bundle multiple messages at the record layer, this was
lost when cyassl i/o was re-implemented but is now fixed.

For general build instructions see rc1 below.

## CyaSSL Release Candidiate 2 rc2-1.0.0 (1/21/2009)


Release Candidate 2 for CyaSSL 1.0.0 adds bug fixes and adds two new stream
ciphers along with their respective cipher suites.  CyaSSL adds support for
HC-128 and RABBIT stream ciphers.  The new suites are:

```
TLS_RSA_WITH_HC_128_SHA
TLS_RSA_WITH_RABBIT_SHA
```

And the corresponding cipher names are

```
HC128-SHA
RABBIT-SHA
```

CyaSSL also adds support for building with devkitPro for PPC by changing the
library proper to use libogc.  The examples haven't been changed yet but if
there's interest they can be.  Here's an example ./configure to build CyaSSL
for devkitPro:

```
./configure --disable-shared CC=/pathTo/devkitpro/devkitPPC/bin/powerpc-gekko-gcc --host=ppc --without-zlib --enable-singleThreaded RANLIB=/pathTo/devkitpro/devkitPPC/bin/powerpc-gekko-ranlib CFLAGS="-DDEVKITPRO -DGEKKO"
```

For linking purposes you'll need

`LDFLAGS="-g -mrvl -mcpu=750 -meabi -mhard-float -Wl,-Map,$(notdir $@).map"`

For general build instructions see rc1 below.


## CyaSSL Release Candidiate 1 rc1-1.0.0 (12/17/2008)


Release Candidate 1 for CyaSSL 1.0.0 contains major internal changes.  Several
areas have optimization improvements, less dynamic memory use, and the I/O
strategy has been refactored to allow alternate I/O handling or Library use.
Many thanks to Thierry Fournier for providing these ideas and most of the work.

Because of these changes, this release is only a candidate since some problems
are probably inevitable on some platform with some I/O use.  Please report any
problems and we'll try to resolve them as soon as possible.  You can contact us
at support@yassl.com or todd@yassl.com.

Using TomsFastMath by passing --enable-fastmath to ./configure now uses assembly
on some platforms.  This is new so please report any problems as every compiler,
mode, OS combination hasn't been tested.  On ia32 all of the registers need to
be available so be sure to pass these options to CFLAGS:

`CFLAGS="-O3 -fomit-frame-pointer"`

OS X will also need -mdynamic-no-pic added to CFLAGS

Also if you're building in shared mode for ia32 you'll need to pass options to
LDFLAGS as well on OS X:

`LDFLAGS=-Wl,-read_only_relocs,warning`

This gives warnings for some symbols but seems to work.


#### To build on Linux, Solaris, *BSD, Mac OS X, or Cygwin:

    ./configure
    make

    from the ./testsuite/ directory run ./testsuite 

#### To make a debug build:

    ./configure --enable-debug --disable-shared
    make



#### To build on Win32

Choose (Re)Build All from the project workspace

Run the testsuite program





# CyaSSL version 0.9.9 (7/25/2008) 

This release of CyaSSL adds bug fixes, Pre-Shared Keys, over-rideable memory
handling, and optionally TomsFastMath.  Thanks to Moisés Guimarães for the
work on TomsFastMath.

To optionally use TomsFastMath pass --enable-fastmath to ./configure
Or define USE_FAST_MATH in each project from CyaSSL for MSVC.

Please use the benchmark routine before and after to see the performance
difference, on some platforms the gains will be little but RSA encryption
always seems to be faster.  On x86-64 machines with GCC the normal math library
may outperform the fast one when using CFLAGS=-m64 because TomsFastMath can't
yet use -m64 because of GCCs inability to do 128bit division.

     *** UPDATE GCC 4.2.1 can now do 128bit division ***

See notes below (0.2.0) for complete build instructions.


# CyaSSL version 0.9.8 (5/7/2008) 

This release of CyaSSL adds bug fixes, client side Diffie-Hellman, and better
socket handling.

See notes below (0.2.0) for complete build instructions.


# CyaSSL version 0.9.6 (1/31/2008) 

This release of CyaSSL adds bug fixes, increased session management, and a fix
for gnutls.

See notes below (0.2.0) for complete build instructions.


# CyaSSL version 0.9.0 (10/15/2007) 

This release of CyaSSL adds bug fixes, MSVC 2005 support, GCC 4.2 support, 
IPV6 support and test, and new test certificates.

See notes below (0.2.0) for complete build instructions.


# CyaSSL version 0.8.0 (1/10/2007) 

This release of CyaSSL adds increased socket support, for non-blocking writes,
connects, and interrupted system calls.

See notes below (0.2.0) for complete build instructions.


# CyaSSL version 0.6.3 (10/30/2006) 

This release of CyaSSL adds debug logging to stderr to aid in the debugging of
CyaSSL on systems that may not provide the best support.

If CyaSSL is built with debugging support then you need to call
CyaSSL_Debugging_ON() to turn logging on.

On Unix use ./configure --enable-debug

On Windows define DEBUG_CYASSL when building CyaSSL


To turn logging back off call CyaSSL_Debugging_OFF()

See notes below (0.2.0) for complete build instructions.


# CyaSSL version 0.6.2 (10/29/2006) 

This release of CyaSSL adds TLS 1.1.

Note that CyaSSL has certificate verification on by default, unlike OpenSSL.
To emulate OpenSSL behavior, you must call SSL_CTX_set_verify() with
SSL_VERIFY_NONE.  In order to have full security you should never do this, 
provide CyaSSL with the proper certificates to eliminate impostors and call
CyaSSL_check_domain_name() to prevent man in the middle attacks.

See notes below (0.2.0) for build instructions.

# CyaSSL version 0.6.0 (10/25/2006) 

This release of CyaSSL adds more SSL functions, better autoconf, nonblocking
I/O for accept, connect, and read.  There is now an --enable-small configure
option that turns off TLS, AES, DES3, HMAC, and ERROR_STRINGS, see configure.in
for the defines.  Note that TLS requires HMAC and AES requires TLS.

See notes below (0.2.0) for build instructions.


# CyaSSL version 0.5.5 (09/27/2006) 

This mini release of CyaSSL adds better input processing through buffered input
and big message support.  Added SSL_pending() and some sanity checks on user
settings.

See notes below (0.2.0) for build instructions.


# CyaSSL version 0.5.0 (03/27/2006) 

This release of CyaSSL adds AES support and minor bug fixes. 

See notes below (0.2.0) for build instructions.


# CyaSSL version 0.4.0 (03/15/2006)

This release of CyaSSL adds TLSv1 client/server support and libtool. 

See notes below for build instructions.


# CyaSSL version 0.3.0 (02/26/2006)

This release of CyaSSL adds SSLv3 server support and session resumption. 

See notes below for build instructions.


# CyaSSL version 0.2.0 (02/19/2006)


This is the first release of CyaSSL and its crypt brother, CTaoCrypt.  CyaSSL
is written in ANSI C with the idea of a small code size, footprint, and memory
usage in mind.  CTaoCrypt can be as small as 32K, and the current client
version of CyaSSL can be as small as 12K.


The first release of CTaoCrypt supports MD5, SHA-1, 3DES, ARC4, Big Integer
Support, RSA, ASN parsing, and basic x509 (en/de)coding.

The first release of CyaSSL supports normal client RSA mode SSLv3 connections
with support for SHA-1 and MD5 digests.  Ciphers include 3DES and RC4.


#### To build on Linux, Solaris, *BSD, Mac OS X, or Cygwin:

    ./configure
    make

    from the ./testsuite/ directory run ./testsuite 

#### to make a debug build:

    ./configure --enable-debug --disable-shared
    make



#### To build on Win32

Choose (Re)Build All from the project workspace

Run the testsuite program



*** The next release of CyaSSL will support a server and more OpenSSL
compatibility functions.


Please send questions or comments to todd@yassl.com
