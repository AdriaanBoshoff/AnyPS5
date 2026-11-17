# libSceLibreSsl3

## add Functional

- [EVP_ecdsa](../../../core/libs/prx/libSceLibreSsl3/src/Ecdsa.cpp) (libSceLibreSsl3) - nothing is checked on the console. LibreSSL 4.0.0 no longer has this digest, but the PS5 3.20 module still exports it, so its fields follow [LibreSSL 2.5.4](https://github.com/libressl/openbsd/blob/2e2c612066aa993717528a0249c15c51128d61cb/src/lib/libcrypto/evp/m_ecdsa.c#L140-L165) `m_ecdsa.c`: type and key type `NID_ecdsa_with_SHA1` (416), a 20-byte SHA-1 output, `EVP_MD_FLAG_PKEY_DIGEST`, `ECDSA_sign` and `ECDSA_verify` in the legacy sign and verify slots, `EVP_PKEY_EC` (408) as the only required key type, a 64-byte block and a 104-byte context. It hashes with libSceLibreSsl's SHA-1 and points the sign and verify slots at libSceLibreSsl's ECDSA functions. This module's `EVP_SignFinal` and `EVP_VerifyFinal` follow 4.0.0 and always sign through the key's method, so they never read those slots. Closes when: compared with the console.
