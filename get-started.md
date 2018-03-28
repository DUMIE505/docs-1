# Get Started

You can run your own instance by following these steps

### Setup

#### Mac OS X

- Install brew: https://brew.sh/
- brew install git (will trigger installation of Xcode, do it!)
- Follow guide https://treehouse.github.io/installation-guides/mac/node-mac.html
- Ready!

### Installation

```sh
git clone git@github.com:proofofexistence/proofofexistence.git
cd proofofexistence
npm install
```

#### Configuration

```sh
npm run setup
```

Edit `.env` for environment variables. All values are **required**.

Report to the [config page](config.md) to learn more about config variables.

### Building

```sh
npm run build
```

### Running

```sh
npm start
```

The app will be listening at http://localhost:3003/.

### Testing

Create a `.env.test` file with the desired configuration. It is recommended to
change the database path to a `/tmp` location.

Run the tests with:

```sh
npm test
```

### Development

To run the app in development mode, create a `.env.dev` file with the desired
configuration.

You must use a **Testnet3 wallet** for the public and private keys. It is
recommended to change the database path to a `/tmp` location.

Run the app in dev mode with:

```sh
NODE_ENV=dev npm run watch
```

### Production

Build the app:

```sh
npm run build
```

The production app is run with:

```sh
NODE_ENV=production npm run serve
```

To clean up:

```sh
npm run clean
```

#### ngrok

To test all functionality, the dev app running locally needs to be able to
receive web hook requests from the Internet.

Sign up for an [ngrok](https://ngrok.com) account, download the client, and
connect it to your account. Run `ngrok` with the port from your `.env.test`
file:

```sh
ngrok http 3003
```

Note the "Forwarding" address and run the app with:

```sh
NODE_ENV=development HOST=xxxxxxxx.ngrok.io HOST_SCHEME=https HOST_PORT=443 npm run watch
```

#### Test Certifications

Finally, to certify a document on the testnet blockchain:

1. Create a `.env.dev` file with all your configuration
1. Set up a new testnet wallet and note down the Private Key WIF
1. Fund the testnet wallet, e.g. using a Bitcoin testnet3 faucet
1. Run the app locally in dev mode, with ngrok active
1. Submit a document hash to the running app on localhost
1. Note down the target address for payment
1. Send payment with `node scripts/payment.js PRIVATE_KEY_WIF TARGET_ADDRESS`
1. Wait for the transaction to be confirmed on testnet blockchain


### Webhooks

Webhooks can be purged by running:

```sh
node purge.js
```
