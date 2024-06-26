# Certificate Authority Setup

This repository contains a script to generate a Root CA, an Intermediate CA, and sign a Wireless LAN Controller (WLC) certificate using OpenSSL. 

The certificates are used for securing communication between network devices and FreeRADIUS server.

## Prerequisites

- OpenSSL v1.1.1f or LibreSSL 3.3.6

## Directory Structure

The script will create the following directory structure:

```
c9800_and_intermediate_certs/
├── mkcerts.sh
├── .root_openssl.cnf
├── .intermediate_openssl.cnf
├── .device.cnf
├── root/
│ └── ca/
│ ├── certs/
│ ├── crl/
│ ├── newcerts/
│ ├── private/
│ └── intermediate/
│    ├── certs/
│    ├── crl/
│    ├── csr/
│    ├── newcerts/
│    └── private/
└── .env
```

## Getting Started

1. Clone the Repository

```sh
git clone https://github.com/darwincastro/c9800_and_intermediate_certs.git
cd c9800_and_intermediate_certs
```

2. Run the script:

```sh
./mkcerts.sh
```

## Script Explanation
The `mkcerts.sh` script performs the following tasks:

1. Load Environment Variables:
    Loads environment variables from the .env file.

2. Define Colors for Output:
    Sets up color variables for output messages.

3. Define Directory Structure:
    Defines the working directory and structure for Root CA and Intermediate CA.

4. Create Directory Structure:
    Creates necessary directories and files for Root CA and Intermediate CA.

5. Check OpenSSL Installation:
    Verifies if OpenSSL is installed.

6. Generate ROOT-CA Key and Certificate:
    Generates the ROOT CA key and self-signed certificate.

7. Generate Intermediate CA Key and CSR:
    Generates the Intermediate CA key and certificate signing request (CSR).

8. Sign Intermediate CA with ROOT CA:
    Signs the Intermediate CA CSR with the ROOT CA.
Combine CA Certificates:

9. Combines the Intermediate CA and ROOT CA certificates into a single PEM file.

10. Generate WLC Key and CSR:
    Generates the WLC key and CSR.

11. Sign WLC CSR with Intermediate CA:
    Sign the WLC CSR with the Intermediate CA.

12. Create PFX Bundle:
    Creates a PFX bundle containing the WLC certificate and keys.

13. Validate the PFX Bundle:
    Validate the generated PFX bundle.


> The mkcerts.sh creates a PKCS#12 bundle in the working directory called WLC-CA.pfx it contains the WLC key, WLC certificate, ROOT CA certificate, and Intermediate CA certificate. The script will also combine ROOT CA and Intermediate CA placing it in the working directory for quick access.



> [!IMPORTANT]  
> - Ensure the .root_openssl, .device.cnf, .intermediate.cnf, and .env configuration files are correctly set up and present in the same directory as the script.
> - The script assumes the password specified in the .env file is cisco. Adjust the password as needed.



## Troubleshooting
If you encounter any issues, ensure that:

- OpenSSL is installed and accessible.
- The .env file is correctly formatted and placed in the root directory.
- The configuration files are correctly set up.

## License

This project is licensed under the MIT License. See the [LICENSE](./LICENSE) file for details.

