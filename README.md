# My GPG Notes

## Renew GPG on Expiration

1. Clone this repo into a working area

    ```bash
    git clone <repo> gpg-renew
    cd gpg-renew
    direnv allow
    ```

    **NOTE:** Skip `direnv` if you are not familier in using it

1. Extract/Place GPG secret key into the directory. Example: `my-secretkey.pem`

1. (If using `direnv`, skip this) Setup `GNUPGHOME` environment variable KEY_ID and PRIVATE_KEY

    ```bash
    export GNUPGHOME=$PWD/.gpg
    ```

    OR use your shell specific syntax

1. Run `gpg-renew-prepare` with key id and private key file name as arguments

    ```bash
    scripts/gpg-renew-prepare yogendrarampuria-secretkey.pem
    ```

1. Follow instruction in the [renew page](RENEW.md) to renew expiry

1. Finalize the (Publish and clean up) key

    ```bash
    scripts/gpg-renew-finalize yogendrarampuria-secretkey.pem
    ```

1. Delete working area

    ```bash
    cd ..
    rm -rf gpg-renew
    ```
