# local-ledger-wasm
Used for local testing rosetta-api.

1. Run local replica
   `dfx start --background --clean`

   - take down the local replica's port
2. Deploy the wasm and mint an account some local ICP token
   
   ```bash
   rm -rf .dfx &&
   dfx deploy \
            --argument "record { minting_account = \"ea2d973e67dcbcb00f1cfb36d05d600eef68c7513c18dac8ef52d165c1d38c36\"; initial_values = vec { record { \"9512b526263c0c1b89b891704e85066f10e08ec11b9639e8ae71b40290436be9\"; record { e8s = 18446744073709551615 } } }; max_message_size_bytes = null; transaction_window = null; archive_options = null; send_whitelist = vec {}}" \
            --network=local \
            --no-wallet \
            ledger
    ```

    - account is minted to "9512b526263c0c1b89b891704e85066f10e08ec11b9639e8ae71b40290436be9"
    - key phrase is "steel obey anxiety vast clever relax million girl cost pond elbow bridge hill health toilet desk sleep grid boost flavor shy cry armed mass"
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
    # --ic-url http://192.168.3.11:59786
    ```

    - the ledger canister id
    - local machine ip, use static ip, not 127.0.0.1 and use replica's port, not 8000
    - wait for `You are all caught up to block 0` hint, then you are good to go