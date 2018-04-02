# Configuration


To get started, copy the `sample-local.yaml` to `local-development.yaml` and edit it.

**All values are required** - except for mail and nodemailer.

---

* `app`
  * `url`
    * `scheme` - e.g. `http` or `https`.
    * `host` - The host or domain name. (`NOTE: you maybe need to use ngrok`)
    * `port` - The local port to run the app on.
  * `magicNumber` - Token for some private API routes.
  * `site` - name of your website
  * `logo` - absolute URL of your logo image

* `db`
  * `path` - Path to the LevelDB directory.

* `currencies` - different currencies accepted by the app
    * `btc` - default to BTC
      * `defaultNetwork` - Default bitcoin network for Bitcore. Options are `livenet` or `testnet`.
      * `networks` - list of networks to be used
        * `incomingPrivateKey` - HD wallet private key to handle incoming payments.
        * `outgoingPublicKey` - HD wallet public key to accept outgoing payments.
        * `documentPrice` - Document certification price in satoshis.
        * `feeMultiplier` - Multiply estimated fee by this value to change its priority. Defaults to `2`.

* `services`
  * `blockcypher` -  we use blockcypher API
    * `token` - BlockCypher API token, Register it [here](https://www.blockcypher.com/).
    * `url`: default API url https://api.blockcypher.com/v1

* `mail`
  * `from` - Name/email to send as.
  * `to` - Email address to send notifications to.

* `nodemailer` - Node service to send email - see [the docs](https://nodemailer.com/about/)
  * `options`:
    * `service` :
    * `auth` :
      * `user` - GMail account for sending notifications.
      * `pass` - Gmail password for sending notifications.

---

We use [node-config](https://github.com/lorenwest/node-config/wiki/Configuration-Files) to manage config files. This will generate a `.env` file in the root folder for environment variables. Any environment variables that are set when the app is run will override the values in the `.env` file.


### About wallets

**Note**: You must create two different HD wallets. The first wallet is the
*Incoming* wallet, which is used to generate payment addresses for the user, and
to sign transactions embedding docproofs. The second wallet is the *Outgoing*
wallet, which is used to generate addresses where the change from docproof
transactions is sent.

The private key for the *Incoming* wallet must be the `BITCOIN_HD_PRIVATE_KEY`.

The public key for the *Outoing* wallet must be `BITCOIN_HD_PUBLIC_KEY`. The
private key for the change wallet should be kept secret, and can be used later
to sweep the funds.

You can use [bcwallet](https://github.com/blockcypher/bcwallet/) to easily create a new wallet.
