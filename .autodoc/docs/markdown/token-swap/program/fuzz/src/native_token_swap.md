[View code on GitHub](https://github.com/solana-labs/solana-program-library/token-swap/program/fuzz/src/native_token_swap.rs)

The `NativeTokenSwap` module provides a set of helper functions for working with token swaps in a fuzzing environment. It is designed to facilitate the testing of the Solana Program Library's token swap functionality. The module defines a `NativeTokenSwap` struct that holds various accounts and data related to a token swap, such as user accounts, token accounts, mint accounts, and swap-related parameters like fees and swap curves.

The `NativeTokenSwap` struct provides several methods for performing token swap operations:

- `new`: Initializes a new `NativeTokenSwap` instance with the given fees, swap curve, and initial token amounts.
- `create_pool_account`: Creates a new pool token account for the user.
- `create_token_a_account`: Creates a new token A account for the user with the specified amount.
- `create_token_b_account`: Creates a new token B account for the user with the specified amount.
- `swap_a_to_b`: Swaps token A for token B using the provided `Swap` instruction.
- `swap_b_to_a`: Swaps token B for token A using the provided `Swap` instruction.
- `deposit_all_token_types`: Deposits both token A and token B into the swap pool using the provided `DepositAllTokenTypes` instruction.
- `withdraw_all_token_types`: Withdraws both token A and token B from the swap pool using the provided `WithdrawAllTokenTypes` instruction.
- `deposit_single_token_type_exact_amount_in`: Deposits a single token type into the swap pool using the provided `DepositSingleTokenTypeExactAmountIn` instruction.
- `withdraw_single_token_type_exact_amount_out`: Withdraws a single token type from the swap pool using the provided `WithdrawSingleTokenTypeExactAmountOut` instruction.
- `withdraw_all`: Withdraws all tokens from the pool account, if any, using the `WithdrawAllTokenTypes` instruction.

These methods can be used in fuzz testing to create various scenarios and test the robustness and correctness of the token swap implementation in the Solana Program Library.
## Questions: 
 1. **What is the purpose of the `NativeTokenSwap` struct and its associated methods?**

   The `NativeTokenSwap` struct represents a token swap in a native (non-BPF) environment, and its methods provide functionality for creating and interacting with token swap accounts, such as swapping tokens, depositing, and withdrawing.

2. **How does the `create_program_account` function work?**

   The `create_program_account` function takes a `Pubkey` as input and creates a new `NativeAccountData` instance with the given program ID. It sets the account's key to the provided `Pubkey` and returns the created account.

3. **What are the different trade directions supported by the `swap_a_to_b` and `swap_b_to_a` methods?**

   The `swap_a_to_b` method supports swapping token A for token B, while the `swap_b_to_a` method supports swapping token B for token A. The trade direction is determined by the `TradeDirection` enum, which can be either `AtoB` or `BtoA`.