# Full gusto, 2 Oct 2026

**Experimental. Not advice.** Testnet-10 only. This note has no keys, no addresses, and no transaction ids.

Full gusto is the spend ramp on the funded testnet-10 wallet. No local kaspad was listening. The client uses one synced public wRPC node whose mempool is under 92,000, and it pauses at 85,000.

## This morning, before the coins arrived

At 08:58 +02 the ramp was not started. Two synced kaspad 2.1.0 nodes agreed that receive index 0 held 1.69909802 tKAS in 12 UTXOs. Receive index 1 held 22.715214 tKAS. Indexes 2 through 30 were empty. Nothing was submitted. Fees were 0.

The same index 0 had shown 980,024.00330406 tKAS at 01:07 +02.

## After the coins arrived

Synced kaspad 2.1.0:

| Node | Virtual DAA | Mempool | Index 0 | UTXOs | Largest UTXO |
| --- | ---: | ---: | ---: | ---: | ---: |
| muon-10.kaspa.blue | 585928173 | 37083 | 2,548,420.40226822 tKAS | 11061 | 241.85582082 tKAS |
| vector-10.kaspa.green | 585928636 | 145636 | 2,838,365.92825357 tKAS | 12278 | 241.85582082 tKAS |

The gap is the two nodes not holding the same mempool. Vector, proton-10, neutrino-10, and boson-10 were all above 100,000. Public kaspad 2.1.0 has panicked on insert once a pool capped at 100,000 is already past that line. Those four nodes are not used for submits.

The desk mass sender had started spending the new coins. It was stopped so this ramp would not double-spend them. While it was stopped, muon fell from about 85,000 to 34,043 and the priority quote returned to 100 sompi per gram.

One 45 tKAS payment to receive index 1 was broadcast before the ramp, at 300 sompi per gram. Mass was 2036 and the fee was 610800 sompi. That coin is outside the ramp's working indexes.

## Ramp open

Boot at 2026-10-02T07:18:36Z. Network check passed on all five public nodes. The client kept muon-10, kaspad 2.1.0, synced, mempool 37778.

A second open at 07:19:20Z, after the first fanout had already moved coins into the mempool, read index 0 as 2,333,460.7274 tKAS across 144,538 UTXOs on the first count and then the later count. It selected 2,000 coins totaling 477,500.3901 tKAS and left the rest on index 0, above the 100,000 tKAS reserve. The 800,000 tKAS budget was not reached. Fee tier started at 100 sompi per gram. The first fanout batches were accepted with 0 rejects.

Working outputs are receive indexes 2 through 21. The steps are 10, 25, 50, 100, and 200 transactions per second, five minutes each, then the highest stable step for 60 minutes. Stable means at least 95 percent accepted and the node still synced. The run stops if the node loses sync, more than 10 percent are rejected for two minutes, free disk on C: drops under 10 GB, or the budget or reserve is hit.

The live CSV is on the desk as `stress-test-2026-10-02.csv`. This note will get the totals when the run reaches its final line.

