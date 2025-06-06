# GeyserBench

A Yellowstone Geyser gRPC endpoint benchmarking tool.

## Overview

GeyserBench is a performance testing tool that connects to multiple Solana gRPC endpoints simultaneously and measures their speed and reliability in detecting transactions.

## Features

- Connect to multiple gRPC endpoints simultaneously
- Measure endpoint performance metrics:
    - First detection rate
    - Average delay
    - Median and 95th percentile latency
- Simple summary output for quick comparison
- Detailed metrics for in-depth analysis

## Installation

### Download Binary

Download the latest release from the [releases page](https://github.com/solstackapp/geyserbench/releases).

## Configuration

When first run, GeyserBench will create a default `config.toml` file. Edit this file to customize your benchmark:

```toml
[config]
transactions = 100
account = "7dGrdJRYtsNR8UYxZ3TnifXGjGc9eRYLq9sELwYpuuUu"
commitment = "processed"

[[endpoint]]
name = "endpoint 1"
url = "https://api.mainnet-beta.solana.com:10000"
x_token = "YOUR_TOKEN_HERE"

[[endpoint]]
name = "endpoint 2"
url = "http://frankfurt.omeganetworks.io:10000"
x_token = ""

[[endpoint]]
name = "endpoint 3"
url = "http://newyork.omeganetworks.io:10000"
x_token = "YOUR_TOKEN_HERE"
```

### Configuration Options

- `transactions`: Number of transactions to measure
- `account`: Account address to monitor for transactions
- `commitment`: Transaction commitment level (processed, confirmed, finalized)
- `endpoint`: Array of gRPC endpoint configurations:
    - `name`: Name for the endpoint
    - `url`: gRPC endpoint URL
    - `x_token`: Authentication token (if required)

## Usage

1. Run GeyserBench to generate the default config:
   ```bash
   ./geyserbench
   ```

2. Edit the generated `config.toml` file with your endpoint details

3. Run the benchmark:
   ```bash
   ./geyserbench
   ```

## Output

GeyserBench provides both simplified and detailed output:

### Simple Summary
```
Finished tests results
endpoint 1: Win rate 85.23%, avg delay 0.00ms (fastest)
endpoint 2: Win rate 10.45%, avg delay 42.31ms
endpoint 3: Win rate 4.32%, avg delay 78.56ms
```

### Detailed Metrics
```
Detailed tests results
----------------------------------

Fastest Endpoint: endpoint 1
  First detections: 82 out of 97 valid transactions (84.54%)
  
Delays relative to fastest endpoint:
endpoint 2:
  Average delay: 42.31 ms
  Median delay: 38.75 ms
  95th percentile: 62.18 ms
  Min/Max delay: 12.45/89.32 ms
  Valid transactions: 97
```
