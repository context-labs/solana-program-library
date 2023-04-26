[View code on GitHub](https://github.com/solana-labs/solana-program-library/token/js/examples/immutableOwner.ts)

This code demonstrates how to create and initialize a custom token mint and associated token accounts on the Solana blockchain using the `solana-program-library`. The code is written as an asynchronous self-invoking function that performs the following steps:

1. Establish a connection to the Solana devnet using the `Connection` class from `@solana/web3.js`.
2. Generate a new keypair for the payer and request an airdrop of 2 SOL to the payer's public key.
3. Generate a new keypair for the mint authority and create a new custom token mint with a specified number of decimals using the `createMint` function. The mint is created using the `TOKEN_2022_PROGRAM_ID` as the program ID.
4. Calculate the minimum balance required for rent exemption for an account with the `ImmutableOwner` extension using the `getAccountLen` and `getMinimumBalanceForRentExemption` functions.
5. Generate keypairs for the owner and the token account, and create a new transaction that includes the following instructions:
   - Create a new account with the required lamports and space for the token account using the `SystemProgram.createAccount` instruction.
   - Initialize the token account with the `ImmutableOwner` extension using the `createInitializeImmutableOwnerInstruction` function.
   - Initialize the token account with the mint and owner public keys using the `createInitializeAccountInstruction` function.
6. Send and confirm the transaction using the `sendAndConfirmTransaction` function from `@solana/web3.js`.
7. Create an associated token account for the owner using the `createAccount` function.

This code can be used as a starting point for developers looking to create custom tokens and associated accounts on the Solana blockchain using the `solana-program-library`.
## Questions: 
 1. **Question:** What is the purpose of the `TOKEN_2022_PROGRAM_ID` constant and where is it defined?
   **Answer:** `TOKEN_2022_PROGRAM_ID` is a constant representing the program ID for the token being created in this script. It is imported from the '../src' module.

2. **Question:** What does the `createInitializeImmutableOwnerInstruction` function do and what are its parameters?
   **Answer:** The `createInitializeImmutableOwnerInstruction` function creates an instruction to initialize an account with an immutable owner. It takes the account public key, the token program ID, and optionally an extension type as its parameters.

3. **Question:** What is the purpose of the `ExtensionType.ImmutableOwner` parameter in the `getAccountLen` function call?
   **Answer:** The `ExtensionType.ImmutableOwner` parameter is used to specify the type of account extension that should be considered when calculating the account length. In this case, it indicates that the account has an immutable owner.