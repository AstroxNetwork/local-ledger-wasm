# local-ledger-wasm
Used for local testing rosetta-api.

1. Run local replica
   `dfx start --background --clean`

   - take down the local replica's port
2. Deploy the wasm and mint an account some local ICP token
   
   ```bash
   dfx deploy \
            --argument "record { minting_account = \"ea2d973e67dcbcb00f1cfb36d05d600eef68c7513c18dac8ef52d165c1d38c36\"; initial_values = vec { record { \"a8a3746fca2b69ee144224ab735b0c0f1977d3aa44a97c75240da7ab05becea4\"; record { e8s = 18446744073709551615 } } }; max_message_size_bytes = null; transaction_window = null; archive_options = null; send_whitelist = vec {}}" \
            --network=local \
            --no-wallet \
            ledger
    ```

    - Initial minting account is "ea2d973e67dcbcb00f1cfb36d05d600eef68c7513c18dac8ef52d165c1d38c36"
    - Private key is "07acb84879d371491ceccb357322b264fc7703e7966686c0fd4d39cebcaffab3"
    - take down the "ledger" canister id.

    Use above for testing transaction

3. Run Rosetta-api, [document here](https://sdk.dfinity.org/docs/integration/ledger-quick-start.html), pay attention to the IP down there, use it for your LAN network.
    

    ```bash
    docker run \
    --interactive \
    --tty \
    --publish 8080:8080 \
    --rm \
    dfinity/rosetta-api \
    --canister-id rwlgt-iiaaa-aaaaa-aaaaa-cai \
    --ic-url http://192.168.3.11:59786
    ```

    - the ledger canister id
    - local machine ip, use static ip, not 127.0.0.1 and use replica's port, not 8000
    - wait for `You are all caught up to block 0` hint, then you are good to go