[View code on GitHub](https://github.com/solana-labs/solana-program-library/token/js/examples/createMintAndTransferTokens.ts)

This code demonstrates how to create, mint, and transfer a custom token on the Solana blockchain using the `solana-program-library`. The code is written as an asynchronous self-invoking function that performs the following steps:

1. **Connect to the cluster**: Establish a connection to the Solana devnet using the `Connection` class from the `@solana/web3.js` package.

```javascript
const connection = new Connection(clusterApiUrl('devnet'), 'confirmed');
```

2. **Generate a wallet and airdrop SOL**: Create a new wallet keypair and request an airdrop of 1 SOL to the wallet.

```javascript
const fromWallet = Keypair.generate();
const fromAirdropSignature = await connection.requestAirdrop(fromWallet.publicKey, LAMPORTS_PER_SOL);
```

3. **Wait for airdrop confirmation**: Confirm the airdrop transaction.

```javascript
await connection.confirmTransaction({
    signature: fromAirdropSignature,
    ...(await connection.getLatestBlockhash()),
});
```

4. **Generate a new wallet for receiving tokens**: Create another wallet keypair to receive the newly minted tokens.

```javascript
const toWallet = Keypair.generate();
```

5. **Create a new token mint**: Create a new token mint with 9 decimal places using the `createMint` function.

```javascript
const mint = await createMint(connection, fromWallet, fromWallet.publicKey, null, 9);
```

6. **Create associated token accounts**: Create or get the associated token accounts for both the sender and receiver wallets.

```javascript
const fromTokenAccount = await getOrCreateAssociatedTokenAccount(connection, fromWallet, mint, fromWallet.publicKey);
const toTokenAccount = await getOrCreateAssociatedTokenAccount(connection, fromWallet, mint, toWallet.publicKey);
```

7. **Mint tokens**: Mint 1 token (represented as 1000000000 due to 9 decimal places) to the sender's token account.

```javascript
let signature = await mintTo(connection, fromWallet, mint, fromTokenAccount.address, fromWallet.publicKey, 1000000000, []);
console.log('mint tx:', signature);
```

8. **Transfer tokens**: Transfer the minted token to the receiver's token account.

```javascript
signature = await transfer(connection, fromWallet, fromTokenAccount.address, toTokenAccount.address, fromWallet.publicKey, 1000000000, []);
console.log('transfer tx:', signature);
```

This code can be used as a reference for developers who want to create, mint, and transfer custom tokens on the Solana blockchain using the `solana-program-library`.
## Questions: 
 1. **Question:** What is the purpose of the `@solana/web3.js` import and how is it used in this code?
   **Answer:** The `@solana/web3.js` import is a JavaScript library for interacting with the Solana blockchain. In this code, it is used to connect to the cluster, generate keypairs, request airdrops, and confirm transactions.

2. **Question:** What does the `createMint` function do and what are its parameters?
   **Answer:** The `createMint` function creates a new token mint on the Solana blockchain. Its parameters are `connection`, `fromWallet`, `mintAuthority`, `freezeAuthority`, and `decimals`. It returns a promise that resolves to the newly created mint.

3. **Question:** How does the `getOrCreateAssociatedTokenAccount` function work and what are its parameters?
   **Answer:** The `getOrCreateAssociatedTokenAccount` function checks if a token account exists for a given wallet address and mint. If it does not exist, it creates one. Its parameters are `connection`, `payer`, `mint`, and `owner`. It returns a promise that resolves to the associated token account.