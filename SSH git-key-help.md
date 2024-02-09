
## SSH Key für Github.com generieren

$ ssh-keygen -t ed25519 -C "workingj@pm.me"

## Kopieren des SSH-Keys in den Zwischenspeicher und bei Github einfügen

$ clip < ~/.ssh/id_ed25519.pub

## SSH Zugang Testen & Fingerprint vergleichen:

$ ssh -T git@github.com

    SHA256:uNiVztksCsDhcc0u9e8BujQXVUpKZIDTMczCvj3tD2s (RSA)
    SHA256:br9IjFspm1vxR3iA35FWE+4VTyz1hYVLIE2t1/CeyWQ (DSA – veraltet)
    SHA256:p2QAMXNIC1TJYWeIOttrVc98/R1BUFWu3/LiyKgUfQM (ECDSA)
    SHA256:+DiY3wvvV6TuJJhbpZisF/zLDA0zPMSvHdkr4UvCOqU (Ed25519)

