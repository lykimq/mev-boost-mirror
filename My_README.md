

# My README

## 1. Run the mev-boost

- [Official Relay lists](https://boost.flashbots.net/):
```
Mainnet Relay:

- Flashbots:
  0xac6e77dfe25ecd6110b8e780608cce0dab71fdd5ebea22a16c0205200f2f8e2e3ad3b71d3499c54ad14d6c21b41a37ae@boost-relay.flashbots.net

- Blocknative:
  0x9000009807ed12c1f08bf4e81c6da3ba8e3fc3d953898ce0102433094e5f22f21102ec057841fcb81978ed1ea0fa8246

- Eden Network
  0xb3ee7afcf27f1f1259ac1787876318c6584ee353097a50ed474f120269c77d3f36169c6939e88eb1a637d0e96dd0b5f3@relay.edennetwork.io
```

1. Run the mev-boost with the relay flashbots:
```
./mev-boost -relay-check -relay https://0xac6e77dfe25ecd6110b8e780608cce0dab71fdd5ebea22a16c0205200f2f8e2e3ad3b71d3499c54ad14d6c21b41a37ae@boost-relay.flashbots.net
```

For mainnet:
```
./mev-boost -mainnet -relay-check -relay https://0xac6e77dfe25ecd6110b8e780608cce0dab71fdd5ebea22a16c0205200f2f8e2e3ad3b71d3499c54ad14d6c21b41a37ae@boost-relay.flashbots.net
```

Some important flags:

```
- addr string  # Change listen address (default: localhost:18550)
- debug        # Enable debug mode
- relay-check  # Check relay status on startup
- json         # Log in JSON format instead of text
- loglevel string # Set log level (default: info)
```

## Understand the project structure

```
.
├── cli    # CLI for mev-boost
│   ├── flags.go
│   ├── main.go
│   ├── main_test.go
│   └── types.go
├── cmd    # Main entry point for mev-boost
│   ├── mev-boost
│   │   └── main.go
│   └── test-cli
│       ├── beacon.go
│       ├── engine.go
│       ├── main.go
│       ├── README.md
│       ├── requests.go
│       └── validator.go
├── CODE_OF_CONDUCT.md
├── common    # Common utilities
│   └── common.go
├── config    # Configuration handling
│   └── vars.go
├── CONTRIBUTING.md
├── Dockerfile
├── docs    # Documentation
│   ├── audit-20220620.md
│   ├── block-proposal.png
│   ├── geth-pos-privnet.md
│   ├── logo-horizontal-transparent.png
│   ├── logo-horizontal-transparent.svg
│   └── mev-boost-integration-overview.png
├── go.mod
├── go.sum
├── LICENSE
├── main.go    # Main entry point for mev-boost
├── Makefile
├── mev-boost
├── My_README.md
├── README.md    # Official README
├── RELEASE.md
├── scripts    # Scripts for mev-boost
│   └── run_mergemock_integration.sh
├── SECURITY.md
├── server    # Server for mev-boost
│   ├── mock
│   │   ├── mock_relay.go
│   │   ├── mock_relay_test.go
│   │   ├── mock_types.go
│   │   └── mock_types_test.go
│   ├── params    # Parameters for mev-boost
│   │   └── paths.go
│   ├── service.go    # Service for mev-boost
│   ├── service_test.go
│   ├── types    # Types for mev-boost
│   │   ├── errors.go
│   │   ├── relay_entry.go
│   │   ├── relay_entry_test.go
│   │   └── U256str.go
│   ├── utils.go    # Utilities for mev-boost
│   └── utils_test.go
├── staticcheck.conf
├── test-cli    # Test CLI for mev-boost
└── testdata    # Test data for mev-boost
    └── signed-blinded-beacon-block-deneb.json

13 directories, 49 files
```

## Add new tests to understand the code

Run and tests:

```
make build
make test
```

### server/service.go

`service/service_test.go`:
- Test Malformed Relay URLs  `TestMalformedRelayURLs` (The URL validation is in the function `NewBoostService` and it only checks for `errNoRelays`).

- The actual URL validation is in the function `handleGetHeader` where it checks the pubkey length.


