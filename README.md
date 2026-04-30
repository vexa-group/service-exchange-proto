# service-exchange-proto

Protobuf definitions and gRPC contracts for the Exchange Service

## Directory Structure

- `proto/`: Contains the source `.proto` files defining the service API and messages.
- `gen/`: Contains the generated code from the proto definitions.
  - `go/`: Generated Go code.
  - `python/`: Generated Python code.

## Services Overview

This repository defines the following gRPC services:

### 1. ExchangeService (`exchange.proto`)

Manages exchange-level operations and data.

- **CreateExchange**: Creates a new exchange.
- **UpdateExchange**: Updates an existing exchange.
- **DeleteExchange**: Deletes an exchange.
- **GetExchange**: Retrieves exchange details.
- **ListExchanges**: Lists exchanges with pagination and filtering.
- **ListProviderCoins**: Lists coins provided by an exchange.
- **CreateProvider**: Adds a new provider configuration for an exchange.
- **GetProvider**: Retrieves provider details.
- **ListProviders**: Lists providers for an exchange.
- **UpdateProvider**: Updates a provider configuration.
- **DeleteProvider**: Removes a provider configuration.

### 2. CoinService (`coin.proto`)

Manages coin and token information across all exchanges.

- **CreateCoin**: Creates a new coin/token definition.
- **UpdateCoin**: Updates coin/token information.
- **DeleteCoin**: Deletes a coin/token.
- **GetCoin**: Retrieves coin/token details.
- **ListCoins**: Lists coins/tokens with filtering and pagination.
- **GetCoinPair**: Retrieves details of a specific coin pair.
- **ListCoinPairs**: Lists coin pairs across all exchanges.
- **UpdateStatus**: Updates the status of a coin or coin pair.
- **SearchCoins**: Searches for coins by name or symbol.
- **GetSymbol**: Retrieves coin/token information by symbol.
- **UploadLogo**: Uploads a logo for a coin.

### 3. MarketService (`market.proto`)

Manages market data including tickers and order books.

- **GetTicker**: Retrieves the current ticker (24h) for a market.
- **ListTickers**: Lists tickers across markets.
- **GetOrderBook**: Retrieves the order book (bids and asks) for a market.
- **ListMarkets**: Lists markets with filtering and pagination.

### 4. OrderService (`order.proto`)

Handles order placement and management.

- **CreateOrder**: Places a new order.
- **CancelOrder**: Cancels an existing order.
- **GetOrder**: Retrieves order details.
- **ListOrders**: Lists orders with filtering and pagination.

### 5. TradeService (`trade.proto`)

Manages trade history and data.

- **ListTrades**: Lists trades with filtering and pagination.
- **GetTrade**: Retrieves trade details.
- **SyncTrades**: Syncs trades from providers.
- **GetHistoricalTrades**: Retrieves historical trades for a market.
- **StreamTrades**: Streams live trade updates for a market.

### 6. Common Definitions (`common.proto`)

Contains shared message definitions used across multiple services:

- **Pagination**: Standard pagination request parameters (page, limit, sort).
- **Meta**: Pagination response metadata (total items, total pages).
- **Success**: A simple success boolean response.

## Installation

### 1. Install Protocol Buffers compiler

**For Ubuntu/Debian:**

```bash
sudo apt-get install protobuf-compiler
```

**For macOS:**

```bash
brew install protobuf
```

### 2. Install Go plugins

```bash
make go-deps
```

### 3. Install Poetry (for Python support)

**For Linux/macOS:**

```bash
curl -sSL https://install.python-poetry.org | python3 -
```

Then install Python dependencies:

```bash
make py-deps
```

## Usage

To generate the Go code from the proto definitions, run the following command from the root of the repository:

```bash
make go
```

This command will:

1. Create the `gen/go` directory if it doesn't exist.
2. Compile all `.proto` files in the `proto/` directory.
3. Output the generated Go code into `gen/go`, preserving the package structure defined by `go_package`.

### Python Code Generation

To generate Python code from the proto definitions:

```bash
make py
```

This command will:

1. Ensure Python dependencies are installed (`make py-deps`)
2. Create the `gen/python` directory if it doesn't exist
3. Compile all `.proto` files using Python's gRPC tools
4. Run a post-processing script to organize the code into service-based directories
5. Output the generated Python code into `gen/python/service_exchange_proto/`

The generated Python package is named `service_exchange_proto` and can be installed from GitHub:

```bash
# Install latest from main branch
pip install git+https://github.com/vexa-group/service-exchange-proto.git

# Install specific version tag
pip install git+https://github.com/vexa-group/service-exchange-proto.git@v1.0.0
```

### Generate Both Go and Python

To generate code for both languages:

```bash
make all
```

## Key Commands

| Command        | Description                            |
| -------------- | -------------------------------------- |
| `make deps`    | Install all dependencies (Go + Python) |
| `make go-deps` | Install Go protobuf plugins only       |
| `make py-deps` | Install Python dependencies via Poetry |
| `make go`      | Generate Go code                       |
| `make py`      | Generate Python code                   |
| `make all`     | Generate both Go and Python code       |
| `make clean`   | Clean all generated code directories   |
