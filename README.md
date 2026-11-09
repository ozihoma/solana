# SolanaSDK

SolanaSDK is a C++ library for working with Solana from Arduino-based ESP32
projects. It is included in this PlatformIO project as a local library and is
configured for the `nodemcu-32s` board.

The SDK provides building blocks for Solana public keys, keypairs and
signatures, hashes, instructions, messages, transactions, and a partial JSON-RPC
connection client. The current connection implementation supports retrieving a
recent blockhash and sending a transaction.

## Requirements

- PlatformIO Core or the PlatformIO IDE extension
- An ESP32 board supported by the `espressif32` PlatformIO platform
- Wi-Fi access for RPC operations

PlatformIO installs the project dependencies listed in `platformio.ini`,
including ArduinoJson, libsodium, and Crypto.

## Build and upload

From the project directory:

```sh
pio run
pio run -t upload
pio device monitor
```

The project is configured for a NodeMCU-32S, uses the Arduino framework and
C++17, and sets the serial monitor speed to 115200 baud. Adjust the environment
in `platformio.ini` if you are using a different ESP32 board or upload port.

## Using the SDK

The library is located in `lib/SolanaSDK/src/SolanaSDK`. Include the headers
you need from your PlatformIO application, for example:

```cpp
#include "SolanaSDK/public_key.h"
#include "SolanaSDK/transaction.h"
```

The SDK's classes are currently in the global C++ namespace. A public key can
be parsed from its Base58 representation:

```cpp
auto address = PublicKey::fromString("11111111111111111111111111111111");
if (address.has_value()) {
    // Use address.value()
}
```

For RPC use, construct a `Connection` with a Solana JSON-RPC endpoint and call
the supported methods, such as `getLatestBlockhash()` and `sendTransaction()`.
Configure Wi-Fi connectivity in the application before making network
requests. Keep keypairs and secret-key material private; do not commit them to
source control.

## Project layout

- `platformio.ini` - PlatformIO board, framework, compiler, and dependency configuration
- `src/` - Example application entry point
- `lib/SolanaSDK/` - Solana SDK library sources and PlatformIO metadata
- `test/` - PlatformIO test directory

The SDK is an in-progress implementation; consult the headers in
`lib/SolanaSDK/src/SolanaSDK` for the currently available API.
