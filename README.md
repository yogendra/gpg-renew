# My GPG Notes

## Renew GPG on Expiration

1. Clone this repo into a working area

    ```bash
    git clone <repo> gpg-renew
    cd gpg-renew
    direnv allow
    ```

2. Create `.envrc.secret` file by copying `.envrc.secrets.example`

    ```bash
    cp .envrc.secrets.example .envrc.secret
    ```

    Edit `.envrc.secrets` and set 
    - **OP_GPG_VAULT** : Name of the 1Password vault where item containing GPG keys, certs and passwords are stored
    - **OP_GPG_ITEM_UUID** : 1Password item UUID

3. Run `gpg-renew-auto` with key id (yogendrarampuria) and extension month(s) (6) as arguments

    ```bash
    scripts/gpg-renew-auto yogendrarampuria 6
    ```
4. Delete working area. Delete .gpg and exported files (*.pem, new and backup)(To added to script after testing few times)


    ```bash
    rm -rf .gpg *.pem
    ```


## Add support for another credential store

Create script/program and configure `CREDS_HOOK` environment variable with full path to it.

The program should work with following arguments 
1. `password`: Sends the key master password output to stdout.
2. `restore` : Restores keys and certs into current folder before renewal.
   1. <KEY_NAME>.secretkey.pem - Current secret key / private key
   2. <KEY_NAME>.publickey.pem - Current certificate
   3. <KEY_NAME>.revocationcert.pem - Current revocation certificate
3. `backup`  : Backs-up certs after the renewal is done
   1. <KEY_NAME>-<TIMESTAMP>.publicjey.pem - Expired / Old public key
   2. <KEY_NAME>-<TIMESTAMP>.revocationcert.pem - Expired / Old revocation certificate
   3. <KEY_NAME>.publickey.pem - New public key / certificate
   4. <KEY_NAME>.revocationcert.pem - New revocation certificate



