# Whitepaper: Paper-Based Voting Supported by Blockchain

Ingo R. Keck, Version 1.0 from 2017-09-30, translate to English by perplexity.ai

## Status Quo

For decades, free and secret elections with voter registers, paper ballots, and supervised counting have proven to be the best method for obtaining a correct and verifiable result.

Currently, an election in Germany proceeds as follows:

- Every voter is recorded in a voter register.
- When a voter wants to vote, they are given a paper ballot, which they fill out in secret.
- The voter is marked as "voted" in a numbered paper voter register, then they may place their folded ballot into the ballot box.
- After the voting period ends, the ballot boxes are opened under supervision and the votes inside are counted.
- The polling station can be observed by election observers both during voting and counting.
- Recounts or multiple counts for verification are easily possible.
- The local election official certifies the local result and passes it on to the central election official.
- The central election official publicly announces the total result and the local results.
- Local election officials can again verify whether their local result was counted correctly.
- The public can check whether the total result was correctly calculated from the published individual results.

In principle, this system is designed and implemented to be very secure. The possibility of subsequent verification is present at all stages.

## Possible Attacks on the Status Quo

The following attack possibilities are conceivable:

- The voter register is altered. Major changes here are risky for fraudsters, as the absolute number of voters (residents over 18) is publicly known and can be easily checked. The number of ballots cast must match the number of people marked as having voted. Actual ballots cast can be easily counted by present election observers. For postal voting, completed postal ballot applications must be available (which can also be checked).
- Voters are prevented from voting. This would become known very quickly through the affected voters.
- Votes are counted incorrectly during the tally. This can be prevented and uncovered by present election observers and controlled recounts.
- Fraud in transmitting results to the central election official: In principle, the local election official can verify the transmitted result on the day of publication.
- Fraud in calculating the total result: The public can verify this.

Centralized digital attacks on the system are not possible thanks to the paper basis and local control.

In fact, most previously detected election frauds have involved forged ballots for real voters (usually postal votes, as in[1]), where the fraudster could be sure they would not go to vote. Such fraud is generally difficult to detect if carried out on a small scale.

There is, however, another weak point in this system: the transmission of correct results from the local level to the central election official. Here, only a few people can verify correctness (the local election official and those helpers/observers who monitored the entire count), verification must occur some time after the election (days or weeks later), and it is likely perceived as an additional effort that is often omitted.

Recently, a study by the CCC revealed that this last weak point-the data transmission-is technically unsecured and thus easily vulnerable. [2] Therefore, in this article, I propose using transparent and secure technologies at this point.

[1] Hessenschau: Kommunalwahl in Kelsterbach - Verdacht auf Wahlbetrug in mehr als 30 Fällen [http://www.hessenschau.de/politik/verdacht-auf-wahlbetrug-in-kelsterbach-in-ueber-30-faellen,kelsterbach-wahlbetrug-100.html](http://www.hessenschau.de/politik/verdacht-auf-wahlbetrug-in-kelsterbach-in-ueber-30-faellen,kelsterbach-wahlbetrug-100.html)

[2] Bericht: Analyse einer Wahlsoftware [https://ccc.de/system/uploads/230/original/PC-Wahl\_Bericht\_CCC.pdf](https://ccc.de/system/uploads/230/original/PC-Wahl_Bericht_CCC.pdf)

## Blockchain-Based Result Reporting

The proposed solution keeps the election process as it is. Only the reporting of local results to the public and the central election official is done through a public, transparent, and cryptographically secured system, so that fraud can be easily detected by anyone.

The central requirements:

- The local election official reports the local result immediately after counting, publicly and cryptographically secured, to the central election official.
- Local helpers can confirm the local result.
- The local election official can immediately verify the local report and confirm the verification.

These requirements are met by the following system:

- Before the election, the list of local election officials and their public keys is published on a public blockchain (digitally signed by the central election official, whose identity and public key are also known).
- The local result is digitally signed by the local election official and published on a public blockchain (machine-readable and with photographed paper documents).
- Local helpers can also publish their signed confirmation on the same blockchain.
- The local election official can also sign and publish the confirmation of result verification on the blockchain.
- The public can read the blockchain, check the signatures, and aggregate the correct results to the total result.

In practice, the full lists and documents will not be published on the blockchain, but rather their digital signatures (e.g., SHA256), and the actual documents will be made available elsewhere under their signatures. IPFS (ipfs.io) offers a simple and secure solution for this.

## Practical Implementation

The system consists of two programs, which must be open source for transparency:

1. A local, secured client ("Signer") that allows:
    - Creation of a password-protected key pair
    - Export of the public key
    - Signing of result reports
    - Signing of photos/scans
    - Creation of signed blockchain transactions containing references to the data
    - Creation of signed data packages for export, which are published by the second program

This local client should only be run on a secured computer with a freshly installed system and no internet access. Data exchange is only for export to the second program. Exporting the private key should not be possible.

2. A local client ("Reporter") with internet access, which allows:
    - Receiving signed data packages from the signer program
    - Testing the signatures
    - Forwarding blockchain transactions from these data packages
    - Publishing the signed documents from the signer program
    - Reading, accessing, and verifying data published on the blockchain and IPFS, also from other polling stations

### Election Process

1. Before the election, the central election official, each local election official, and local election helpers (if desired) generate a key pair with the signer program and report the public key to the central election official.
2. The central election official creates a list of all public keys, signs it with their signer program, and publishes it with the reporter program on IPFS and the blockchain.
3. Each local election official creates a result report with the signer program and attaches photos of the paper documents. All files are signed by them.
4. Each local election official publishes these files with the reporter program on IPFS and the blockchain.
5. Local election helpers can check the report within minutes with their reporter program and confirm the verification with the signer program (and then report it with the reporter program).
6. Anyone can monitor the blockchain and read and verify results with a local installation of the reporter program or other programs.

## Expected Difficulties

This project presents several challenges:

### User-Friendliness

The strict separation between the signer and reporter systems is desirable for security reasons. At the same time, data transfer in one direction is necessary. This transfer must be as user-friendly as possible without creating a security risk. The data to be transferred is not large, so it could be transferred via Bluetooth or USB stick, though these methods introduce security risks.

If the strict separation is abandoned, a smartphone app would be suitable for the signer program, as photos can be easily taken there. On iOS, the private key could also be securely stored on the phone. On Android, this is generally not possible.
In any case, help from UX experts is needed to make both programs easy to use.

### Funding

There is existing software with known security vulnerabilities for this problem. It is unclear whether the public sector is contractually bound to continue paying for and using this software. It is highly unlikely that it would be willing to financially support an open source project as an alternative. The best option seems to be seeking funding through foundations or prototype tenders and, once the solution exists, creating public pressure for its adoption.

### Public Perception

This project will only be noticed by the public if the issue is brought to public attention. Dedicated public relations work is needed for this, which also incurs costs.

### Security

The signer program is the security weak point in the system. The reporter program is relatively uncritical, as it can at most suppress data from the signer program or make it appear forged. Both would quickly be noticed and would not affect the final result.
