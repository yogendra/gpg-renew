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
   1. <keyid>-<date>.publickey.pem (Backup of old cert)
   2. <keyid>-<date>.revocationcert.pem (Backup of old revocation key)
   3. <keyid>.revocationcert.pem
   4. <keyid>.publickey.pem

5. Delete working area. Delete .gpg and exported files (*.pem, new and backup)

    ```bash
    rm -rf .gpg *.pem
    ```


## Clean up Docs

1. Secret key: Unchanged. No Need to Store. Just delete local copy
2. Public Key: Changed. Backup and delete
   1. Add <keyname>-<timestamp>.publickey.pem to Credential Repo / **archive**
   2. Delete Credential Repo / Live / <keyname>.publickey.pem
   3. Add <keyname>.publickey.pem to Credential Repo / **live**
3. Revocation Cert Changed. Backup and delete
   1. Add <keyname>-<timestamp>.revocationcert.pem to Credential Repo / **archive**
   2. Delete Credential Repo / Live / <keyname>.revocationcert.pem
   3. Add <keyname>.revocationcert.pem to Credential Repo / **live**
