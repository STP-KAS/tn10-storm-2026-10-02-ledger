# Full gusto, 2 Oct 2026

**Experimental. Not advice.** Testnet-10 only. This note has no keys, no addresses, and no transaction ids.

Full gusto is a hosted tic-tac-toe run: first-seat wins, second-seat wins, and draws, then claims. It is not the mass sender. The host is the public tic-tac-toe guest. This repo did not submit those transactions and did not run the guest.

## What was already true this morning

At 08:58 +02 a spend ramp was not started. Two synced kaspad 2.1.0 nodes agreed that receive index 0 held 1.69909802 tKAS in 12 UTXOs. Receive index 1 held 22.715214 tKAS. Indexes 2 through 30 were empty. The mempool had no incoming outputs to index 0. The ramp needed 600,000 tKAS in the split and a 100,000 tKAS reserve. Nothing was submitted. Fees for that attempt were 0.

The same index 0 had shown 980,024.00330406 tKAS at 01:07 +02, while the desk mass sender was still running.

## Coins present when this run opened

A later read, after the new coins had arrived, still on synced kaspad 2.1.0:

| Node | Virtual DAA | Mempool | Index 0 | UTXOs | Largest UTXO |
| --- | ---: | ---: | ---: | ---: | ---: |
| muon-10.kaspa.blue | 585928173 | 37083 | 2,548,420.40226822 tKAS | 11061 | 241.85582082 tKAS |
| vector-10.kaspa.green | 585928636 | 145636 | 2,838,365.92825357 tKAS | 12278 | 241.85582082 tKAS |

Index 1 was unchanged at 22.715214 tKAS, and its largest coin was 0.997727 tKAS, short of a 1.5 tKAS join. The gap between the two index-0 totals is the two nodes not holding the same mempool. Vector's pool was already past 100,000. Public kaspad 2.1.0 has panicked on insert once a pool configured for 100,000 transactions is already past that line, so this run does not submit to a node at or above 85,000, and it waits to resume until a pool is back under 70,000.

At the same moment proton-10, neutrino-10, and boson-10 each reported a mempool around 400,000 and stayed synced. Those pools are above the 100,000 panic line, so they were not used.

## Brake, then open

The first launch hit `mempool_brake` and submitted nothing. Muon was at about 85,000 and the other public nodes were higher.

Muon then fell while the mass sender was held:

| Time (UTC) | Mempool | Normal | Priority |
| --- | ---: | ---: | ---: |
| 07:13:10 | 45944 | 195 | 901 |
| 07:13:26 | 34448 | 190 | 601 |
| 07:13:41 | 34095 | 100 | 100 |
| 07:13:56 | 34043 | 100 | 100 |

The match client opened on muon-10 at virtual DAA 585933084. The node was synced, network `testnet-10`, mempool 34057, priority 100 sompi per gram. The second-seat fund is 45 tKAS at three times that quote, 300 sompi per gram. Mass was 2036 and the fee was 610800 sompi.

The slate is 30 matches: 12 meant to end First, 9 Second, and 9 Draw. Stake is 1 tKAS. Carrier transactions stay on encoder 0.1.6, which has no feerate argument. On the earlier ten-match run those floors were create 228300, join 227300, each turn 181100, and withdraw 181800 sompi. If a create does not appear on the host, the slate stops instead of opening another game.

Claims use the owning seat, start at 969600 sompi, and on a relay-minimum rejection resubmit at three times the required amount.

Match lines and claim rows will be added here when the run finishes. Until then the local client is still playing.
