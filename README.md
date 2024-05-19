# My GPG Notes

## Renew GPG on Expiration

1. Clone this repo into a working area

    ```bash
    git clone <repo> gpg-renew
    cd gpg-renew
    ```

2. Extract/Place GPG secret key into the directory. Example: `<keyname>.secretkey.pem`

3. Run `gpg-renew-auto` with key id (yogendrarampuria) and extension month(s) (6) as arguments

    ```bash
    scripts/gpg-renew-auto yogendrarampuria 6
    ```

4. Store away cert and revocation cert in safe place.
   1. <keyid><date>.secretkey.pem (Backup of old key)
   2. <keyid><date>.publickey.pem (Backup of old cert)
   3. <keyid><date>.revocationcert.pem (Backup of old revocation key)
   4. <keyid>.revocationcert.pem
   5. <keyid>.publickey.pem

5. Delete working area. Delete .gpg and exported files (*.pem, new and backup)

    ```bash
    rm -rf .gpg *.pem
    ```
