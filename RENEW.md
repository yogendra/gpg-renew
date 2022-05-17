# Extend your keys

This is based on writeup on [this blog][source-blog].

At this point you have an isolated GnuPG home area. Now follow the step below to extend expiry for your key and sub keys

1. Execute the `export` commands from the `gpg-renew-prepare` output

    ```bash
    export KEY_ID=############
    export GNUPGHOME=/tmp/gpg-renew/.gnupg
    ```

1. Edit your key

    ```bash
    gpg --edit-key $KEY_ID
    ```

    Output:

    ```log

    gpg (GnuPG) 2.2.27; Copyright (C) 2021 Free Software Foundation, Inc.
    This is free software: you are free to change and redistribute it.
    There is NO WARRANTY, to the extent permitted by law.

    Secret key is available.

    sec  rsa4096/<KEY_ID>
        created: 2019-05-10  expires: 2021-05-10  usage: SC
        trust: unknown       validity: unknown
    ssb  rsa2048/<SUB_KEY_1_ID>
        created: 2019-05-10  expired: 2021-01-04  usage: E
    ssb  rsa2048/<SUB_KEY_2_ID>
        created: 2019-05-10  expired: 2021-01-04  usage: SA
    [ unknown] (1). John Doe <johndoe@email.com>
    ```

1. Set new expire for primary key

    ```bash
    expire
    ```

    Output:

    ```log
    Changing expiration time for the primary key.
    Please specify how long the key should be valid.
            0 = key does not expire
          <n>  = key expires in n days
          <n>w = key expires in n weeks
          <n>m = key expires in n months
          <n>y = key expires in n years
    Key is valid for? (0)
    ```

    Enter new expiry duration. Example: `3m`

    ```bash
    3m
    ```

    Output:

    ```log
    Key expires at Tue 11 May 01:39:29 2021 +08
    Is this correct? (y/N)
    ```

    Type `y`

    ```bash
    y
    ```

    Output:

    ```log
    sec  rsa4096/<KEY_ID>
        created: 2019-05-10  expires: 2021-05-10  usage: SC
        trust: unknown       validity: unknown
    ssb  rsa2048/<SUB_KEY_1_ID>
        created: 2019-05-10  expired: 2021-01-04  usage: E
    ssb  rsa2048/<SUB_KEY_2_ID>
        created: 2019-05-10  expired: 2021-01-04  usage: SA
    [ unknown] (1). John Doe <johndoe@email.com>


    gpg: WARNING: Your encryption subkey expires soon.
    gpg: You may want to change its expiration date too.
    ```

1. Set expiry for sub-key

    ```bash
    key 1
    ```

    Output:

    ```log
    sec  rsa4096/<KEY_ID>
        created: 2019-05-10  expires: 2021-05-10  usage: SC
        trust: unknown       validity: unknown
    ssb* rsa2048/<SUB_KEY_1_ID>
        created: 2019-05-10  expired: 2021-01-04  usage: E
    ssb  rsa2048/<SUB_KEY_2_ID>
        created: 2019-05-10  expired: 2021-01-04  usage: SA
    [ unknown] (1). John Doe <johndoe@email.com>

    ```

    Notice the `*` after the `ssb`. It mean you are operating on that key

    ```bash
    expire
    ```

    Output:

    ```log
    Changing expiration time for a subkey.
    Please specify how long the key should be valid.
            0 = key does not expire
          <n>  = key expires in n days
          <n>w = key expires in n weeks
          <n>m = key expires in n months
          <n>y = key expires in n years
    Key is valid for? (0)
    ```bash
    Enter expiry time. Example:
    ```

    Enter `3m`

    ```bash
    3m
    ```

    Output:

    ```log
    Key expires at Tue 11 May 01:46:10 2021 +08
    Is this correct? (y/N)
    ```

    Choose `y`

    ```bash
    y
    ```

    Output:

    ```log
    sec  rsa4096/<KEY_ID>
        created: 2019-05-10  expires: 2021-05-10  usage: SC
        trust: unknown       validity: unknown
    ssb* rsa2048/<SUB_KEY_1_ID>
        created: 2019-05-10  expires: 2021-05-10  usage: E
    ssb  rsa2048/<SUB_KEY_2_ID>
        created: 2019-05-10  expired: 2021-01-04  usage: SA
    [ unknown] (1). John Doe <johndoe@email.com>

    ```

    Unselect key 1

    ```bash
    key 1
    ```

    Output:

    ```log
    sec  rsa4096/<KEY_ID>
        created: 2019-05-10  expires: 2021-05-10  usage: SC
        trust: unknown       validity: unknown
    ssb  rsa2048/<SUB_KEY_1_ID>
        created: 2019-05-10  expires: 2021-05-10  usage: E
    ssb  rsa2048/<SUB_KEY_2_ID>
        created: 2019-05-10  expired: 2021-01-04  usage: SA
    [ unknown] (1). John Doe <johndoe@email.com>

    ```

1. Repeat above step for the rest of the keys

1. After this save and exit

    ```bash
    save
    ```

[source-blog]: https://blog.josefsson.org/2014/08/26/the-case-for-short-openpgp-key-validity-periods/#more-782
