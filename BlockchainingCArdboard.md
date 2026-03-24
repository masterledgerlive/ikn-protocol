# BLOCKCHAINING CARDBOARD 
### Decentralized Multi-Factor Authentication for Physical Assets and Creator IP

> **Status:** Architecture / Pre-Development — Smart contract development pending.
> This README serves as the canonical architectural blueprint for contributors and AI coding agents building on this protocol.

---

## Table of Contents

1. [Abstract](#abstract)
2. [Core Architecture: Lock, Key, and Sleeve](#core-architecture-lock-key-and-sleeve)
3. [The Multi-Layer Obfuscation Stack](#the-multi-layer-obfuscation-stack)
   - [Layer 0 — The Compiler Layer](#layer-0--the-compiler-layer)
   - [Layer 1 — The Steganographic Data Layer](#layer-1--the-steganographic-data-layer)
   - [Layer 2 — The Honeypot / False Data Layer](#layer-2--the-honeypot--false-data-layer)
   - [Layer 3 — The Negative Space Hard Key](#layer-3--the-negative-space-hard-key)
4. [The Negative Space Key Protocol](#the-negative-space-key-protocol)
5. [Deterministic Display Key Rotation (Option B)](#deterministic-display-key-rotation-option-b)
6. [Proof Flow: Ownership Verification vs. Transfer](#proof-flow-ownership-verification-vs-transfer)
7. [The 40-Second HTLC Trading Mechanism](#the-40-second-htlc-trading-mechanism)
8. [Creator Ecosystem and The Fan Viewer](#creator-ecosystem-and-the-fan-viewer)
9. [Smart Contract Data Schema](#smart-contract-data-schema)
10. [Primitive Glossary](#primitive-glossary)
11. [Recommended Blockchain Infrastructure](#recommended-blockchain-infrastructure)
12. [Threat Model](#threat-model)
13. [Known Open Problems](#known-open-problems)
14. [Contributor Notes for AI Coding Agents](#contributor-notes-for-ai-coding-agents)

---

## Abstract

The current physical collectibles market relies on centralized grading systems and static authenticity markers, making it structurally vulnerable to sophisticated forgery and single-point-of-failure attacks. The **Proof of Truth (PoT) Protocol** solves this by transforming any physical asset into a dynamic, self-describing cryptographic document.

The protocol achieves this through four stacked layers of authentication embedded directly into the physical object — visible to the eye, but practically unbreakable in combination. Layer 0 acts as a self-contained compiler: it describes the schema for reading all deeper layers. Layers 1 and 2 blend rich metadata with deliberately planted false data (honeypots) at a configurable ratio. Layer 3 secures the asset using a **Negative Space Key** — a cryptographic commitment derived not from what data is *present*, but from a precisely defined *absence pattern*, making full visual possession of the card insufficient to reconstruct the key.

Ownership proofs use **Deterministic Display Key Rotation**: each scan generates a new visual pattern derived from a seed, so the output changes with every verification event while the underlying commitment remains constant. Transfer events burn the Hard Sleeve Key and atomically remint a new one for the buyer's wallet via a **Hash Time-Locked Contract (HTLC)** with a 40-second dual-scan window.

The protocol also functions as a decentralized creator studio, allowing independent artists to mint, license, and embed rich media layers — including live stats, video highlights, and interactive games — directly into physical objects via the **Fan Viewer** AR layer.

---

## Core Architecture: Lock, Key, and Sleeve

The protocol separates every physical asset into three distinct cryptographic roles:

| Role | Description | Mutability |
|---|---|---|
| **The Substrate (Lock)** | The physical object. Contains the multi-layer encoded data including public schema, steganographic metadata, honeypot data, and negative space key anchors. | Immutable |
| **The Ephemeral Sleeve Key** | A cryptographic hash stored on-chain and paired to the Substrate. Destroyed on transfer, reminted for the new owner. | Ephemeral |
| **The ZKP Intersection** | When an owner scans the Substrate, the system reads the physical layers and generates a Zero-Knowledge Proof confirming ownership without exposing the master key combination. | Stateless |

The Substrate is **public and permanent**. The Sleeve Key is **private and ephemeral**. The ZKP is the bridge between them that requires neither party to trust the other.

---

## The Multi-Layer Obfuscation Stack

Each physical card in any set or sub-tokenized series contains five stacked layers. These layers are physically co-located — they occupy the same visual space on the card — but are cryptographically distinct. An attacker who fully decodes one layer gains no structural advantage on any deeper layer.

| Layer | Name | Shared Across Set? | Unique Per Card? | Mutable? |
|---|---|---|---|---|
| 0 | Compiler Layer | ✅ Same schema for whole set | ❌ | ❌ Immutable |
| 1 | Steganographic Data | ✅ Same structure, different values | Partial | ❌ Immutable |
| 1.5 | **Universal Unique Identity (Card DNA)** | ❌ Never shared or reused | ✅ One per card, ever | ❌ Permanent |
| 2 | Honeypot / False Data | ✅ Same FDR range | ❌ | ❌ Immutable |
| 3 | Negative Space Hard Key | ❌ | ✅ Unique per ownership event | ✅ Rotates on transfer |
| V | **Value State Layer** | ❌ | ✅ Card-specific | ✅ Dynamic |

> **Design principle for variants:** Every card that shares the same image is still a completely distinct digital object. Same picture. Different Card DNA. Different Negative Space Key. Different Value State. The protocol treats a common penny card and a 1/1 with equal cryptographic seriousness — both have permanent unique identity, both have authenticated ownership history, both can carry a mystery prize allocation.

---

### Layer 0 — The Compiler Layer

**Visibility:** Fully human and machine readable. Intentionally public.

Layer 0 is the self-describing schema of the card. Like a compiler receiving its own instruction set, this layer tells any reader — human, AI agent, or scanning application — exactly how to parse all subsequent layers. It contains:

- The encoding method used in Layer 1 (e.g., CMYK halftone offset, hex color delta, number sequence modulation)
- The grid resolution and sampling points for the physical scan
- The false data ratio range for Layer 2 (min/max %, not the exact value)
- The negative space anchor coordinate system used in Layer 3
- The set identifier and sub-tokenization series root hash
- The creator wallet address and royalty basis points

**Design principle:** Knowing the compiler instructions does not let you forge the card. It only tells you how to *read* a legitimate one. The instructions are the legend; the data they describe is locked in deeper layers.

---

### Layer 1 — The Steganographic Data Layer

**Visibility:** Optically present but not plaintext. Requires Layer 0 schema to parse.

Layer 1 contains the rich metadata payload of the asset. It is encoded using any combination of:

- CMYK dot pattern offsets (halftone noise modulation)
- Hex color value deltas in defined pixel regions
- Numeric sequences embedded in fine-print or border geometry
- UV-reactive ink patterns readable under specific spectrum lighting

This layer contains:

- Asset provenance chain (mint date, creator, edition number)
- IPFS/Arweave content identifier (CID) for off-chain media assets
- Fan Viewer unlock parameters
- On-chain contract address and token ID
- Substrate commitment hash (the on-chain anchor for the Negative Space Key)

Layer 1 data is **blended with Layer 2 false data** at the physical print level, making it impossible to isolate Layer 1 values without first resolving the false data ratio — which requires a valid Sleeve Key.

---

### Layer 1.5 — The Universal Unique Identity Layer (Card DNA)

**Visibility:** Not directly readable. Committed on-chain at mint. Permanent and irrevocable.

Layer 1.5 is the answer to: *"Of the thousands of cards printed with this image, which specific physical object is this one?"* It is generated exactly once — at the moment of physical printing — and exists nowhere else in the history of the protocol. It cannot be regenerated, rotated, or transferred. It is the card's genetic identity, not its ownership record.

**Generation:** Card DNA is derived from a combination of print-time physical entropy and protocol state:

```
card_dna = hash(
  print_entropy_sample     ← micro ink dispersion, paper fiber variance at print moment
  || set_id
  || card_serial_index
  || mint_timestamp
  || creator_salt
)
```

This hash is stored on-chain as the **Card DNA Commitment** at mint and never updated. Even two cards from the same print run of the same image — printed seconds apart on the same machine — are distinguishable at this layer because the physical entropy sample is unique to each print event.

**Key properties:**
- The penny card has a Card DNA. The 1/1 has a Card DNA. Every card in every set has a Card DNA.
- Perfect visual replication of a card's surface cannot replicate its Card DNA — the print-time entropy is physically non-reproducible
- Card DNA persists through every ownership transfer. The Sleeve Key rotates; the Card DNA never does.
- Card DNA is the permanent anchor linking a specific physical object to its entire provenance chain, from first mint to current owner

---

### Layer 2 — The Honeypot / False Data Layer

**Visibility:** Indistinguishable from Layer 1 without a valid key.

Layer 2 is deliberately planted decoy data intermixed with Layer 1 at a ratio defined per-card at mint time. This ratio — the **False Data Ratio (FDR)** — is itself part of the Sleeve Key configuration and is never stored in plaintext on-chain.

Key properties:

- An attacker who fully decodes the visual surface of the card sees a combined Layer 1 + Layer 2 output with no clear boundary between real and false data
- The FDR ranges are published in Layer 0 (e.g., "between 30% and 70% of data points are false"), but the exact ratio for any given card is only resolvable with the Sleeve Key
- False data points are structurally valid — they pass format checks and appear internally consistent, functioning as cryptographic traps

**Security implication:** An attacker attempting to brute-force Layer 1 must simultaneously solve for the FDR, multiplying the search space by the size of the false data field at every attempt.

---

### Layer 3 — The Negative Space Hard Key

**Visibility:** Not directly visible. Defined by the absence of data at specific coordinates.

Layer 3 is the most novel component of the protocol. The Hard Sleeve Key is not encoded in any data *present* on the card. It is derived from a precisely defined **absence pattern**: specific coordinates in the card's data grid that are intentionally left empty, and whose emptiness encodes the key.

This means:

- Full 4K optical capture of the card surface does not reveal the key
- Sharing a high-resolution image of the card as proof of ownership does not expose the key
- The visible data on the card — including all of Layers 0, 1, and 2 — actively misdirects any reconstruction attempt because the key lives in what is *not there*

The on-chain **Substrate Commitment** stores a hash of the negative space coordinate set. During verification, the scanner reads the card, confirms the expected absences match the on-chain commitment via ZKP, and the proof is accepted without the coordinate set ever being transmitted.

---

## The Value State Layer

Every card carries a living value state that exists independently of any marketplace listing. Value is not assigned by an intermediary — it is derived from three possible modes, configured by the creator at mint, and optionally concealed as a mystery prize.

### Mode 1: Floor Value (The Penny)

Every card in the protocol has a minimum verified floor value, even if that floor is $0.01. This is not symbolic. It means the card is authenticated, has a verified provenance chain, and is a confirmed participant in the network. The penny *is* the proof. A card with a penny floor is not worthless — it is a cryptographically verified physical object with a permanent unique identity and a complete ownership history.

### Mode 2: Fair Market Value (Mathematical Derivation)

For sets where the creator enables dynamic pricing, each card's value is derived on-chain from its variant's supply and demand state:

```
fair_value = (total_variant_pool_value / circulating_supply_of_variant)
             × rarity_weight
             × demand_coefficient
```

Where `demand_coefficient` is calculated from the 30-day scan velocity for that variant — how frequently cards of this type are being scanned, traded, or verified. This gives every card a living price that reflects actual market behavior rather than arbitrary listing prices.

The formula is transparent, auditable, and runs entirely on-chain. No oracle or off-chain pricing feed is required for the base calculation.

### Mode 3: Mystery Prize Allocation

At mint time, the creator allocates a prize pool across the set. A configurable subset of cards — say 1 in every 500, or 3 in every set of 100 — receive a hidden bonus value above their face value. The allocation works as follows:

- The prize pool total and eligible card count are committed to on-chain at mint (provably fair and publicly auditable)
- Which specific cards hold prizes is determined by verifiable random function (VRF) at mint and stored as encrypted commitments — not revealed until triggered
- **Reveal condition:** The mystery prize unlocks only when the current rightful owner scans the card and produces a valid ownership ZKP
- Prize types are configurable: monetary value, exclusive media unlock, physical redemption code, or an upgrade to a higher-tier card in the same set
- Cards holding mystery prizes are **visually identical** to non-prize cards of the same variant. There is no external indicator.

```json
"mystery_allocation": {
  "pool_total_usd": 500.00,
  "eligible_card_count": 10,
  "selection_method": "VRF_AT_MINT",
  "prize_type": "MONETARY | MEDIA | REDEMPTION | UPGRADE",
  "reveal_condition": "valid_ownership_ZKP_by_current_owner",
  "revealed": false,
  "reveal_block": null
}
```

### Same Image, Different Everything

This is the core design principle for variant sets. Cards that share the same artwork are still completely distinct digital objects in the protocol:

```
SET: "Point Guard — Slam Dunk" — 500 cards printed
│
├── Card #001/500
│     Card DNA:     unique fingerprint
│     Value Mode:   Floor ($0.01)
│     Mystery:      NO
│
├── Card #042/500
│     Card DNA:     unique fingerprint
│     Value Mode:   Floor ($0.01)
│     Mystery:      YES — $50 prize, hidden until owner scans
│
├── Card #099/500
│     Card DNA:     unique fingerprint
│     Value Mode:   Fair Market (dynamic)
│     Mystery:      NO
│
└── Card #500/500
      Card DNA:     unique fingerprint
      Value Mode:   Floor ($0.01)
      Mystery:      NO
```

No two cards in this set share a Card DNA. No two share a Negative Space Key history. Mystery prize cards are indistinguishable from the outside. The protocol treats every card — common or rare — with equal cryptographic seriousness.

---

## The Negative Space Key Protocol

The Negative Space Key operates as a **visual nullifier**, analogous in concept to the ZK nullifiers used in privacy-preserving protocols like Zcash, but applied to physical optical data.

### How It Works

```
CARD PRINTED
│
├── At mint: a set of N coordinate pairs is generated as the absence pattern
├── hash(coordinate_set || creator_salt) → substrate_commitment
├── substrate_commitment is stored on-chain
└── coordinate_set is NEVER stored anywhere — it is the secret

OWNERSHIP PROOF
│
├── Owner scans card at full resolution
├── Scanner reads all data points across the card grid
├── ZKP prover: "I know a coordinate_set S such that
│   (a) all coordinates in S are empty in this scan, AND
│   (b) hash(S || salt) = on-chain substrate_commitment"
├── Proof submitted on-chain
├── Verifier confirms proof WITHOUT seeing S
└── Ownership confirmed

TRANSFER
│
├── Hard Sleeve Key invoked (uses coordinate_set as private input)
├── Key BURNED on-chain in same transaction as remint
└── New coordinate_set generated for buyer → new substrate_commitment stored
```

### Security Properties

| Attack Vector | Outcome |
|---|---|
| Full visual copy of card | Fails — negative space is not optically distinguishable from structural whitespace |
| Replay attack (reuse old scan) | Fails — ZKP includes wallet address and block height as public inputs |
| Brute force coordinate set | Computationally infeasible at N ≥ 32 coordinate pairs on a 4K grid |
| Steal card + scan without key | Fails — scanner cannot generate valid ZKP without knowing which absences are meaningful |

---

## Deterministic Display Key Rotation (Option B)

When an owner **proves ownership without transferring**, the protocol does not burn the Hard Sleeve Key. Instead, it generates a **Display Key** — a non-destructive proof token.

Each Display Key produces a unique visual pattern output, so the visible result of a proof scan changes every time. This means:

- An observer who watches multiple proof events cannot correlate the outputs to reconstruct the underlying key pattern
- The owner can publicly share proof scans without leaking any key material
- The card's visual pattern appears different in every proof event, making timing attacks that attempt to map the key through repeated observation ineffective

### Derivation Function

```
display_key_n = KDF(substrate_commitment || owner_wallet || block_height_at_scan)
```

Where KDF is a standard hash-based key derivation function (e.g., HKDF-SHA256). Each scan at a new block height produces a deterministically different but cryptographically consistent output. The substrate_commitment never changes. The display output always does.

---

## Proof Flow: Ownership Verification vs. Transfer

```
┌─────────────────────────────────────────────────────────────┐
│                    SCAN EVENT                               │
└──────────────────────────┬──────────────────────────────────┘
                           │
              ┌────────────▼────────────┐
              │  Transfer requested?    │
              └────────┬────────────────┘
                       │
          ┌────────────▼──────────────────────┐
         YES                                  NO
          │                                   │
          ▼                                   ▼
  TRANSFER FLOW                      PROOF-ONLY FLOW
  ─────────────                      ───────────────
  Both parties scan                  Owner scans alone
  40-second HTLC window              Layer 0 parses schema
  Layer 0-3 full read                Layers 1+2 confirmed
  Hard Sleeve Key invoked            ZKP generated with:
  ZKP confirms seller ownership        substrate_commitment
  Buyer scan confirms custody          owner_wallet
  Funds released atomically            current block_height
  Seller key BURNED                  Display Key returned
  Buyer key MINTED                   (new pattern, non-destructive)
  Both in same transaction           Hard Sleeve Key untouched
```

---

## The Distribution Ledger & Live Market Intelligence

Every card in the protocol generates a permanent on-chain event record across its entire lifecycle. The ledger is always current, always auditable, and mathematically verifiable by anyone.

### Registered Event Types

| Event | Trigger | On-Chain Data |
|---|---|---|
| `MINT` | Card created | Card DNA commitment, initial value state, VRF prize allocation |
| `PULL` | Pack opened, first owner assigned | Distribution timestamp, first owner wallet |
| `SCAN` | Ownership proof generated | Wallet, block height, display key index |
| `VERIFY` | Condition assessment logged | Grade, defect map CID, verifier ID, confidence score |
| `NEGOTIATE` | Price negotiation session opened | Session ID, suggested price at open, high/mid/low at open |
| `TRADE` | Peer-to-peer HTLC (no funds) | Both wallets, card DNA, block |
| `SALE` | HTLC with funds transfer | Both wallets, card DNA, final agreed price, block |
| `RECERTIFY` | New condition photos + grade | New grade, photo CIDs, verifier co-sign if present |
| `GRADE_DISPUTE` | Owner contests a verification | Dispute ID, disputing wallet, disputed verifier |
| `MYSTERY_REVEAL` | Prize unlocked by rightful owner | Prize type, reveal block (prize value stays private) |

This means at any moment the protocol can answer: *"Of the 500 cards in this set, how many have been pulled? How many have changed hands? What did the last 10 verified sales close at? How many have been graded Mint or better?"* — with a cryptographically verified answer derived from real on-chain events, not estimates.

### Real-Time Three-Tier Market Algorithm

Every variant's price is continuously recalculated from verified closed sales on the network. Unverified listings do not feed the algorithm — only completed, on-chain sales count. The more the network is used, the more accurate and trustworthy the math becomes.

```
HIGH  = 90th percentile of verified closed sales (rolling 90-day window)
MID   = weighted median of verified closed sales × condition_coefficient
LOW   = 10th percentile of verified closed sales (rolling 90-day window)

suggested_price(card) = MID × condition_coefficient(card)
```

**Condition Coefficients:**

| Grade | Coefficient |
|---|---|
| Mint / Gem | 1.00 |
| Near Mint | 0.85 |
| Excellent | 0.70 |
| Good | 0.50 |
| Fair | 0.30 |
| Poor | 0.15 |

The condition coefficient is sourced from the card's most recent verified grade record. A card with no verification history uses the set baseline coefficient until it is graded. This gives owners a direct incentive to certify their cards — a verified Near Mint card commands a materially higher suggested price than an unverified equivalent.

---

## Condition Verification & Recertification

Cards can be verified and recertified at any point in their ownership history. Each verification session produces a permanent condition record linked to the Card DNA — building a living history of the card's physical state across every owner.

### Verification Flow

```
VERIFY / RECERTIFY EVENT
│
├── Owner initiates verification scan
├── Card DNA confirmed ← same physical card since mint
├── Sleeve Key confirmed ← current rightful owner
│
├── AI GRADING PASS (automatic)
│     ├── Corner wear detection
│     ├── Surface scratch and print defect mapping
│     ├── Edge condition analysis
│     ├── Centering measurement
│     └── Output: suggested_grade + defect_map + confidence_score
│
├── PHOTO CAPTURE (stored to IPFS, CID linked to Card DNA on-chain)
│     ├── Front — full card, calibrated lighting
│     ├── Back — full card
│     ├── Corner close-ups ×4
│     └── Defect regions — auto-flagged and cropped by AI
│
├── HUMAN CO-SIGN (optional — raises grade authority level)
│     ├── Any wallet with Verifier Tier ≥ 1 can review AI output and photos
│     ├── Verifier can confirm, adjust grade up/down, or flag for dispute
│     ├── Co-signature commits their reputation stake to this grade
│     └── Higher verifier tier = higher authority weight on the grade
│
└── GRADE COMMITTED ON-CHAIN
      ├── Linked permanently to Card DNA
      ├── Condition coefficient updated
      ├── Suggested price recalculated
      └── Photo CIDs stored (permanent visual record of card at this moment)
```

### Grade History

Every card accumulates a complete grade history tied to its Card DNA. A card that has passed through three owners and been recertified each time has a visible physical biography — you can see how the condition changed (or didn't) across its life. This is more information than any traditional grading service provides.

---

## The Verifier Reputation System

Any wallet can participate in human verification. Trust is earned through volume, accuracy, and consistency of past verifications — and is staked, not just scored. Bad verifications have real consequences on tier standing.

### Verifier Tiers

| Tier | Name | Requirements | Privileges |
|---|---|---|---|
| 0 | Unverified | Default | Buy / sell / scan — no co-sign authority |
| 1 | Community Verifier | 10+ verifications completed, dispute rate < 20% | Co-sign cards with suggested price < $50 |
| 2 | Trusted Verifier | 50+ verifications, dispute rate < 10% | Co-sign cards with suggested price < $500 |
| 3 | Shop Verifier | 200+ verifications, dispute rate < 5% | Co-sign any value — listed on verified shop registry |
| 4 | Protocol Verifier | Invitation + audit + bond deposit | Resolve grade disputes — co-sign high-value 1/1s — audit Tier 3 applicants |

### Reputation Staking

Verification is not free from consequence. When a verifier co-signs a grade:

- Their wallet ID and tier level are permanently linked to that grade record on-chain
- If the grade is later disputed and the dispute is upheld by a Tier 4 arbiter, the verifier's dispute rate increases
- Repeated upheld disputes reduce tier score and can result in tier demotion
- A Tier 3 Shop Verifier who co-signs fraudulent or negligent grades can lose their shop registry listing

This makes the human verification layer self-policing. Verifiers have direct reputational skin in the game on every co-signature they produce.

### Buyer-Initiated Verification

Verification does not have to be owner-initiated. A prospective buyer can request a verification session as part of the purchase negotiation. The seller accepts the request, the card is scanned together, the AI runs its grading pass in real time, and both parties see the result before the HTLC fires. This eliminates the information asymmetry that makes physical card sales adversarial.

---

## In-Scan Price Negotiation

When a buyer and seller initiate a sale event together, the protocol opens a negotiation session before the HTLC clock starts. Both parties see the same verified data at the same time.

### Negotiation Interface

```
┌─────────────────────────────────────────────┐
│  Point Guard — Slam Dunk  #042/500          │
│  Card DNA: Verified ✓   Owner: Verified ✓   │
│                                             │
│  CONDITION                                  │
│  Grade:  Near Mint                          │
│  Source: AI + Tier 3 Shop co-sign           │
│  Certified: 14 days ago                     │
│                                             │
│  MARKET  (23 verified sales — last 90 days) │
│  HIGH    $84.00                             │
│  MID     $61.00   ← suggested               │
│  LOW     $38.00                             │
│                                             │
│  SELLER ASKING    $65.00                    │
│  BUYER OFFER      $58.00                    │
│                                             │
│  [COUNTER]  [ACCEPT MID $61.00]  [WALK AWAY]│
│                                             │
│  ⚠ 40-second HTLC window starts on ACCEPT  │
└─────────────────────────────────────────────┘
```

The negotiation window has no time limit — both parties can counter as many times as they want. The 40-second HTLC clock starts only when both wallets confirm an agreed price. This separates the human negotiation layer from the cryptographic settlement layer cleanly.

### Negotiation Session Record

Every negotiation session — including sessions that end in a walk-away — is logged on-chain as a `NEGOTIATE` event. This data feeds the market algorithm. A pattern of sellers asking far above MID and buyers walking away is a signal the algorithm incorporates into future suggested prices.

---

## The 40-Second HTLC Trading Mechanism

Physical asset trades require confirmed custody transfer, not just wallet-to-wallet token movement. The HTLC enforces this by requiring both a cryptographic proof (on-chain) and a physical scan (off-chain, verified on-chain) within a strict time window.

### State Machine

```
LISTED
  │
  ▼
LOCKED_IN_ESCROW        ← Buyer funds enter smart contract
  │
  ▼
DUAL_SCAN_WINDOW        ← 40-second window opens
  │
  ├── Both scans verified within window?
  │       │
  │      YES                    NO
  │       │                      │
  │       ▼                      ▼
  │   DUAL_VERIFIED          WINDOW_EXPIRED
  │       │                      │
  │       ▼                      ▼
  │   KEY_BURNED             FUNDS_RETURNED
  │       │                  CONTRACT_ABORTED
  │       ▼
  │   KEY_REMINTED (atomic with burn)
  │       │
  │       ▼
  │   SETTLED
  │
  └── KEY_BURNED and KEY_REMINTED are a single atomic transaction.
      No intermediate state where card exists without a valid on-chain key.
```

### Critical Atomicity Requirement

The burn and remint of the Sleeve Key **must execute in a single atomic transaction**. Any implementation that separates these into two transactions creates a race condition window where the physical card exists in custody limbo. Smart contract implementations must enforce this as a hard constraint.

---

## The Burn Mechanism & Deflationary Value Engine

The protocol includes an optional but deeply integrated burn system that transforms card destruction from a loss event into a strategic economic decision. Every card can be burned. Every burn reshapes the value landscape for every surviving card.

### The Physical Burn Ribbon

Each card is manufactured with a hidden burn ribbon embedded along one edge or spine of the physical card. The ribbon:

- Is not optically visible under normal or UV light — it cannot be detected by scanning the intact card surface
- Contains the **Burn Key**, encoded using the same multi-layer steganographic system as the authentication layers
- Is revealed **only** by physically tearing or destroying the card along the burn line
- Once revealed, the Burn Key is a one-time-use string that cannot be reconstructed from the intact card surface or any prior scan data

This design enforces irreversibility at the physical layer. There is no digital shortcut to collect the burn value. The card must actually be destroyed.

### The Three Burn Pool Types

#### Pool Type 1 — Set Burn Pool (Collective Deflationary)

A shared pool exists for every set. Anyone — holder or outside participant — can deposit into this pool at any time. When a card is burned:

```
release_amount = total_set_pool_balance / cards_remaining_in_set
```

After each burn, `cards_remaining` decreases. The next burn releases a larger slice of a pool that may also be growing from new deposits. Early burners receive smaller guaranteed payouts. Late burners receive larger shares from a scarcer, potentially higher-value pool. The math rewards patience but guarantees something for every burn.

#### Pool Type 2 — Creator Pre-Load (Guaranteed Burn Floor)

At mint time, the creator can pre-load a fixed amount into the set burn pool. This establishes a guaranteed minimum burn value for every card before any community deposits occur.

```
Example:
  Creator pre-loads $500 into a 500-card set
  Minimum burn value per card = $500 / 500 = $1.00
  This is already 100× the penny face value
  Every community deposit above this raises the floor further
```

The creator pre-load is committed on-chain at mint and is publicly auditable. Buyers can see the guaranteed burn floor before purchasing any card in the set.

#### Pool Type 3 — Variant Competition Pool (Strategic Pressure)

For sets with multiple copies of the same variant (e.g., 5 copies of a rare image), a separate pool exists for that specific variant. Any holder — including other holders of the same variant — can deposit into this pool to create competitive pressure.

```
Example:
  5 holders own "Gold Slam Dunk" variant
  Holder A deposits $20 into the Gold Slam Dunk variant pool
  Burn value for next burn of this variant: pool share + set pool share

  Holders B, C, D must now decide:
    → Burn and collect now (certain)
    → Hold and hope to be the last survivor (uncertain but higher upside)

  If B, C, D all burn:
    Holder A (who deposited) and Holder E are now holding a 2/5
    One of them is now one burn away from owning the last copy
    The depositor funded their own path to potential 1/1 status
```

This creates a variant-level game where holders simultaneously compete against and strategically cooperate with each other.

### The Live Burn Value Formula

```
burn_value(card) =
  (set_pool_balance / cards_remaining_in_set)     ← collective share
  + variant_pool_balance_for_this_variant          ← competition pool share
  + creator_preload_remaining_share                ← guaranteed floor component
  + hidden_burn_multiplier (if allocated by VRF)   ← revealed only on burn

```

This value is displayed to the card owner in real time and updates continuously as others burn, as new deposits are made, and as the set's circulation count changes. The owner always knows their current guaranteed burn value before deciding.

### The Hidden Burn Multiplier

At mint time, a configurable subset of cards — selected by VRF, committed on-chain, not revealed — receive a hidden burn multiplier embedded in their ribbon. When burned, these cards release more than the formula alone would suggest.

- The existence of multiplier cards is public (the count and range are in the set's Layer 0 schema)
- Which specific cards hold multipliers is not revealed until the ribbon is torn
- This adds an irreducible uncertainty to every hold/burn decision — the penny card in your hand might release 5× the standard burn value

### The 1/1 Emergence Mechanic

Any variant can become a de facto 1/1 through the burn process. The protocol tracks this explicitly and upgrades the surviving card's on-chain status when it happens.

```
VARIANT LIFECYCLE
│
├── 5/5 in circulation    → Standard variant
├── 3/5 in circulation    → Elevated scarcity flag — burn pool visibility increases
├── 2/5 in circulation    → High scarcity — both holders see live competing burn values
└── 1/5 in circulation    → LAST SURVIVOR EVENT
                               ├── Card auto-upgrades to 1/1 status on-chain
                               ├── Card DNA receives permanent LAST_SURVIVOR flag
                               ├── Variant burn pool locks:
                               │     cannot release until holder burns
                               │     OR holder retains indefinitely as true 1/1
                               └── Fan Viewer unlocks exclusive last-survivor content tier
```

A card that achieves Last Survivor status through documented burn history is arguably more valuable than a designed 1/1 — its scarcity is mathematically proven and publicly auditable, not just asserted.

### The Competing Incentive Matrix

No position in the burn system has an obviously dominant strategy. This is intentional.

| Position | Burn Now | Hold | Deposit Into Pool |
|---|---|---|---|
| Common card, early circulation | Small guaranteed payout | High risk, small intrinsic upside | Raises everyone's burn value including your own card's |
| Common card, late circulation | Larger payout, scarcity premium building | Possible Last Survivor emergence | Strategic — could pressure other variant holders |
| Variant holder (e.g., 1/5) | Collect current pool now | Race to be the last survivor | Fund competitive pressure on the other 4 holders |
| Last Survivor (de facto 1/1) | Collect entire remaining pool | Hold a true proven 1/1 permanently | N/A — already won the scarcity race |

The burn system creates a living market dynamic. Every participant's decision — burn, hold, or deposit — changes the calculus for every other participant in real time.

### Burn Event Registration

Every burn is a permanent on-chain event:

```json
"burn_event": {
  "card_dna_commitment": "0x...",
  "variant_id": "GOLD_SLAM_DUNK",
  "edition_number": 3,
  "edition_size": 5,
  "burn_key_hash": "0x...",
  "set_pool_balance_at_burn": 0.00,
  "release_amount": 0.00,
  "hidden_multiplier_applied": false,
  "cards_remaining_after_burn": 4,
  "burn_block": 0,
  "burner_wallet": "..."
}
```

The card DNA and burn key hash are permanently recorded. The physical card is gone. The proof that it existed, who destroyed it, when, and what it was worth at destruction is preserved forever.

---

The PoT Protocol supports **sub-tokenization**, allowing creators to launch independent sets or series under the protocol's security framework without requiring custom cryptographic infrastructure.

### Creator Licensing

Each creator-minted set is a derivative namespace of the PoT root protocol. The creator:

- Designs the Layer 0 schema for their set (encoding method, FDR range, grid resolution)
- Sets royalty basis points baked into the smart contract (enforced on all secondary sales)
- Controls the media assets registered to their Fan Viewer CID
- Retains IP ownership of their artwork; the protocol only controls the authentication layer

Royalty enforcement uses on-chain hooks that fire on every Sleeve Key burn-and-remint event (i.e., every ownership transfer), making secondary market royalties structurally unavoidable rather than voluntary.

### The Fan Viewer (AR / Media Layer)

The steganographic layers do not only authenticate — they function as an **API hook**. When the rightful owner scans their card and a valid ownership ZKP is confirmed, the protocol unlocks the **Fan Viewer**: a dynamic media interface tied to that specific card.

The Fan Viewer can surface:

- Embedded video highlights or exclusive content (served from IPFS/Arweave CID registered at mint)
- Live player statistics via a registered oracle feed (e.g., Chainlink sports data adapter)
- Exclusive community games or interactive experiences
- Real-time ownership provenance history
- Creator messages or unlockable content tiers

**The Fan Viewer is access-gated by the ZKP.** A non-owner who scans the card sees the public Layer 0 data only. The full Fan Viewer unlocks only when the scanner's wallet can produce a valid ownership proof for that specific token.

---

## Smart Contract Data Schema

The following is the canonical on-chain data structure for a PoT asset. All smart contract implementations must conform to this schema.

```json
{
  "asset_id": "PoT-2025-SET001-0042",
  "set_root_hash": "0x...",

  "identity": {
    "card_dna_commitment": "0x...",
    "card_serial_index": 42,
    "variant_id": "POINT_GUARD_SLAM_DUNK",
    "edition_size": 500,
    "print_timestamp": 0
  },

  "authentication": {
    "substrate_commitment": "0x...",
    "sleeve_key_hash": "0x...",
    "sleeve_key_state": "ACTIVE | BURNED | LOCKED_IN_ESCROW",
    "false_data_ratio_range": {
      "min_pct": 30,
      "max_pct": 70
    },
    "layer_0_schema": {
      "encoding_method": "CMYK_HALFTONE_OFFSET | HEX_DELTA | UV_SPECTRUM",
      "grid_resolution": "4096x4096",
      "sampling_points": 2048,
      "negative_space_anchor_system": "CARTESIAN_NORMALIZED"
    }
  },

  "value": {
    "mode": "FLOOR | FAIR_MARKET | CREATOR_SET",
    "floor_value_usd": 0.01,
    "creator_set_value_usd": null,
    "fair_market_params": {
      "rarity_weight": 1.0,
      "demand_window_days": 30
    },
    "mystery_allocation": {
      "pool_total_usd": null,
      "eligible_card_count": null,
      "selection_method": "VRF_AT_MINT",
      "prize_type": "MONETARY | MEDIA | REDEMPTION | UPGRADE",
      "reveal_condition": "valid_ownership_ZKP_by_current_owner",
      "revealed": false,
      "reveal_block": null
    }
  },

  "burn": {
    "burn_ribbon_present": true,
    "burn_key_commitment": "0x...",
    "burn_state": "INTACT | BURNED",
    "burn_block": null,
    "burner_wallet": null,
    "hidden_multiplier_allocated": false,
    "hidden_multiplier_revealed": false,
    "set_pool_balance_at_burn": null,
    "release_amount": null
  },

  "pools": {
    "set_pool_balance": 0.00,
    "set_pool_depositors": [],
    "variant_pool_balance": 0.00,
    "variant_pool_depositors": [],
    "creator_preload": 0.00,
    "cards_remaining_in_set": 500,
    "cards_remaining_in_variant": 5
  },


    "owner_wallet": "...",
    "creator_wallet": "...",
    "royalty_bps": 500
  },

  "media": {
    "fan_viewer_cid": "ipfs://...",
    "static_assets_cid": "ipfs://...",
    "live_data_oracle": "chainlink://..."
  },

  "provenance": {
    "mint_block": 0,
    "mint_timestamp": 0,
    "transfer_count": 0,
    "last_transfer_block": 0
  }
}
```

---

## Primitive Glossary

| Term | Definition |
|---|---|
| **Substrate** | The physical card or object. Immutable once printed. |
| **Compiler Layer (Layer 0)** | The self-describing schema embedded in Layer 0. Tells any reader how to parse deeper layers. Always public. |
| **Steganographic Data Layer (Layer 1)** | Rich metadata and media hooks encoded in the physical surface using the Layer 0 schema. |
| **Honeypot Layer (Layer 2)** | Deliberately planted false data intermixed with Layer 1 at a configurable False Data Ratio. Indistinguishable from Layer 1 without a Sleeve Key. |
| **Negative Space Hard Key (Layer 3)** | Cryptographic key derived from precisely defined *absent* data points on the card surface. Never visually present; resists full optical capture. |
| **False Data Ratio (FDR)** | The percentage of Layer 1+2 data points that are honeypot data. Configurable per card at mint. Never stored in plaintext. Part of the Sleeve Key config. |
| **Substrate Commitment** | On-chain hash of the negative space coordinate set. Verifiable without exposing the coordinates. |
| **Hard Sleeve Key** | The destructive ownership key. Burned on transfer, atomically reminted for the new owner. |
| **Display Key** | Non-destructive proof token. Generated per scan event. Does not burn the Hard Sleeve Key. |
| **Deterministic Display Rotation** | Each Display Key is derived from substrate_commitment + owner_wallet + block_height, producing a unique but consistent output per scan without exposing the underlying key. |
| **Visual Nullifier** | The Negative Space Key's property of being defined by absence, analogous to ZK nullifiers in privacy coin protocols. |
| **Fan Viewer** | AR/media interface unlocked by a valid ownership ZKP. Access-gated. Surfaces dynamic off-chain content tied to the specific asset. |
| **HTLC** | Hash Time-Locked Contract. The 40-second dual-scan trade escrow mechanism. |
| **FDR Range** | Published in Layer 0 as min/max bounds. Exact FDR for a specific card is private. |
| **Universal Unique Identity Layer (Layer 1.5)** | The permanent Card DNA layer. Generated once at print time from physical entropy. Never rotated, never reused. Every card has one, including penny commons. |
| **Card DNA** | The unique cryptographic fingerprint of a specific physical card, derived from print-time entropy. Distinguishes individual cards within the same variant and image. Permanent. |
| **Card DNA Commitment** | On-chain hash of the Card DNA. Stored at mint, never updated. |
| **Value State Layer** | The dynamic per-card value record. Supports floor, fair market, and mystery prize modes. |
| **Floor Value** | Minimum verified value of any card in the protocol. Even a penny floor means the card is authenticated and has provable provenance. |
| **Fair Market Value** | Mathematically derived on-chain price based on variant supply, rarity weight, and 30-day scan velocity demand coefficient. |
| **Mystery Prize Allocation** | Hidden bonus value committed to a random subset of cards at mint via VRF. Indistinguishable externally. Revealed only to the rightful owner upon valid ownership ZKP scan. |
| **VRF** | Verifiable Random Function. Used to select mystery prize cards at mint in a provably fair and publicly auditable way. |
| **Burn Ribbon** | A hidden physical strip embedded in each card containing the Burn Key. Not optically detectable on the intact card. Revealed only by physical destruction. |
| **Burn Key** | One-time-use cryptographic string encoded in the burn ribbon. Released only when the card is physically destroyed. Cannot be reconstructed from the card surface. |
| **Set Burn Pool** | Shared pool for an entire set. Any participant can deposit. Each burn releases a proportional share. Remaining share per card grows as supply decreases. |
| **Creator Pre-Load** | Fixed amount deposited by the creator at mint into the set burn pool. Establishes a guaranteed minimum burn value before any community deposits. |
| **Variant Competition Pool** | A separate burn pool scoped to a specific variant. Holders of the same variant can deposit to create competitive pressure on other holders. |
| **Burn Value** | Real-time calculated payout a card would release if burned. Derived from set pool share + variant pool share + creator preload share + hidden multiplier if allocated. |
| **Hidden Burn Multiplier** | A VRF-allocated hidden bonus applied to a subset of cards at mint. Revealed only when the burn ribbon is torn. Multiplies the standard burn value release. |
| **Last Survivor** | The final remaining copy of a variant after all others have been burned. Auto-upgraded to 1/1 status on-chain with permanent Card DNA flag and exclusive Fan Viewer tier. |
| **1/1 Emergence** | The protocol event triggered when a variant's circulation count reaches 1. Scarcity is mathematically proven through documented burn history — distinct from a designed 1/1. |

---

## Recommended Blockchain Infrastructure

### Primary: Solana

Solana's architecture is the best fit for this protocol's requirements:

- Throughput of 65,000+ TPS supports real-time optical scan verification at scale
- Sub-cent transaction fees make the constant burn-and-remint Sleeve Key cycle economically viable
- Sub-second finality supports the 40-second HTLC window without race condition risk
- Metaplex standard provides a compatible royalty enforcement foundation

### Alternative Layer 2s

**Base (Coinbase L2):** Strong choice for retail user onboarding. Coinbase wallet integration reduces friction for non-crypto-native collectors. Inherits Ethereum's security model.

**Polygon:** Mature ecosystem with established NFT infrastructure. Well-suited for high-volume set releases with predictable gas costs.

### Infrastructure Dependencies

| Component | Recommended Solution |
|---|---|
| Off-chain media storage | IPFS + Arweave (redundant pinning) |
| Live data oracles | Chainlink Data Feeds |
| ZKP system | Groth16 or PLONK (to be finalized in v0.2 spec) |
| Scan attestation | Wallet-signed attestations (not OAuth — see Threat Model) |

---

## Threat Model

### What the Protocol Defeats

| Attack | Defense |
|---|---|
| Physical duplication of card | Layer 2 FDR + Layer 3 negative space are not optically reproducible without the Sleeve Key config |
| Replay attack (reuse prior scan proof) | ZKP public inputs include owner_wallet + block_height, making old proofs invalid |
| Key theft via visual observation | Negative Space Key is not visible — full 4K capture of card does not expose it |
| Display key interception | Display Key is non-destructive and changes every scan; intercept yields nothing reusable |
| Secondary market royalty bypass | Royalty hook fires on every Sleeve Key burn event — structurally enforced, not voluntary |
| Burn key extraction without destruction | Burn Key is in the physically separate ribbon — not present in any layer of the intact card surface, not recoverable from any scan |
| Fake burn claim (claiming burn without destroying card) | Burn Key is one-time-use; on-chain verification confirms it has never been submitted before; physical ribbon cannot be reattached |
| Burn pool manipulation (spam deposits to game release timing) | Pool math is transparent and on-chain; all depositors are public; manipulation is visible and factored into fair value algorithm |

### What the Protocol Does Not Protect Against

- **Coercion:** A valid owner can be compelled to perform a transfer scan under duress
- **Device compromise:** If the scanner device is compromised at the OS level, scan attestation signing may be intercepted
- **Creator key loss:** If a creator loses their wallet, royalty payments continue but creative control of the set metadata is unrecoverable
- **Physical destruction:** The protocol cannot authenticate a card that has been physically destroyed or damaged beyond scan threshold

---

## Known Open Problems

These are open architectural questions to be resolved before v1.0 smart contract deployment:

1. **ZKP system selection:** Groth16 offers smaller proof sizes; PLONK offers universal trusted setup. Decision pending benchmarking on Solana.
2. **Scan hardware standardization:** Layer 0 schema must define a minimum optical resolution and lighting specification for scan validity. Currently undefined.
3. **Negative space coordinate set size (N):** Security analysis needed to define minimum N for the 4K grid to resist brute force at acceptable confidence.
4. **FDR resolution mechanism:** Exact mechanism by which a valid Sleeve Key resolves the FDR from the blended Layer 1+2 output needs formal specification.
5. **Fan Viewer oracle failover:** If a live data oracle feed becomes unavailable, the Fan Viewer should degrade gracefully to static content rather than failing entirely.
6. **Print entropy capture method:** The physical process for sampling and hashing print-time entropy into the Card DNA Commitment needs hardware specification. Candidates include optical ink dispersion sampling, paper fiber interferometry, and registration offset measurement.
7. **Market algorithm bootstrap problem:** The three-tier price algorithm requires sufficient verified sales history to be meaningful. Sets with fewer than ~10 closed sales need a fallback pricing model during early circulation.
8. **Verifier tier bond mechanism:** Tier 4 Protocol Verifiers are described as bonded but the bond amount, custody method, and slashing conditions are not yet defined.
9. **Grade dispute resolution timeline:** When a `GRADE_DISPUTE` is filed, the maximum resolution window for Tier 4 arbiters needs definition to prevent disputes from blocking sales indefinitely.
10. **Walk-away negotiation data privacy:** `NEGOTIATE` events that end in walk-away feed the market algorithm. The granularity of data logged (exact offer amounts vs. range buckets) needs a privacy tradeoff decision.
11. **Burn ribbon manufacturing spec:** The physical method for embedding the burn ribbon invisibly — UV-reactive ink strip, micro-perforated tear line, embedded fiber optic thread — needs a production specification before cards can be printed.
12. **Burn pool smart contract custody:** The set and variant burn pools hold real funds. The custody mechanism (multisig, time-lock, or fully autonomous contract) and upgrade/emergency-drain authority need formal security review before any creator pre-loads funds.
13. **Last Survivor lock timing:** When a variant reaches 1/5 remaining, the variant pool locks. The exact lock trigger (at 1 remaining vs. at 2 remaining to create end-game tension) is a design decision with significant game-theoretic consequences.
14. **Cross-set burn pool deposits:** Whether wallets outside the set (third-party speculators) can deposit into a set's burn pool — increasing the burn value to entice destruction of competitors' cards — needs an explicit policy decision.

---

## Contributor Notes for AI Coding Agents

If you are an AI coding agent reading this README to begin implementation, here is the priority build order and the key constraints you must enforce:

**Build Order:**
1. Smart contract: Asset registration with Card DNA Commitment and Substrate Commitment storage
2. Smart contract: Sleeve Key mint, burn, and atomic burn+remint
3. Smart contract: Distribution Ledger — event registry for all card lifecycle events
4. Smart contract: HTLC escrow with negotiation session + 40-second dual-scan window and state machine
5. Smart contract: Royalty hook on all Sleeve Key burn events
6. Smart contract: Value State — floor, fair market formula, and mystery prize VRF allocation
7. Smart contract: Mystery prize reveal gate (requires valid ownership ZKP, fires once per card)
8. Smart contract: Verifier tier registry — wallet tiers, dispute rate tracking, tier promotion/demotion logic
9. Smart contract: Grade commitment — on-chain grade record linked to Card DNA, co-sign by verifier wallet
10. Smart contract: Three-tier market algorithm — rolling 90-day verified sales, condition coefficient application
11. Off-chain: ZKP prover circuit (negative space coordinate verification + Card DNA confirmation)
12. Off-chain: Display Key KDF (HKDF-SHA256 with substrate_commitment + wallet + block_height)
13. Off-chain: AI grading pipeline — corner wear, surface defect, centering, edge analysis → grade + defect map
14. Client: Layer 0 schema parser
15. Client: In-scan negotiation UI — real-time HIGH/MID/LOW display, offer/counter flow, ACCEPT trigger
16. Client: Fan Viewer unlock gate (requires valid ownership ZKP)
17. Client: Value display — floor, fair market, and mystery prize reveal UI
18. Client: Verifier dashboard — verification queue, co-sign flow, reputation score display
19. Smart contract: Set burn pool — deposit, balance tracking, per-burn release calculation
20. Smart contract: Variant competition pool — scoped deposits, competitive pressure display
21. Smart contract: Creator pre-load at mint — guaranteed floor commitment
22. Smart contract: Burn Key verification and one-time redemption gate
23. Smart contract: Last Survivor detection — auto 1/1 upgrade trigger at variant count = 1
24. Client: Live burn value display — real-time pool balance, release estimate, hold/burn decision UI
25. Client: Variant competition view — show other holders' positions and live variant pool balance

**Hard Constraints:**
- Sleeve Key burn and remint MUST be atomic (single transaction). Never separate these.
- OAuth MUST NOT be used for scan attestation. Use wallet-signed attestations only.
- Display Key generation MUST NOT touch or expose the Hard Sleeve Key.
- FDR exact value MUST NOT appear in any on-chain storage in plaintext.
- ZKP public inputs MUST include owner_wallet and block_height to prevent replay attacks.
- Card DNA Commitment MUST be written at mint and MUST NEVER be updated or overwritten under any condition.
- Mystery prize reveal MUST require a valid ownership ZKP from the current owner. It MUST fire exactly once per card and MUST NOT be reversible.
- Mystery prize eligible card selection MUST use a VRF committed at mint. Manual or post-mint selection is not permitted.
- The three-tier market algorithm MUST only ingest verified closed sales (completed HTLC events). Unverified listings or cancelled negotiations MUST NOT move the HIGH/MID/LOW values.
- Verifier tier promotions MUST be calculated from on-chain event data only. No off-chain or manual tier assignment is permitted above Tier 0.
- The 40-second HTLC clock MUST NOT start until both parties have confirmed an agreed price in the negotiation session. Negotiation and settlement are separate phases.
- Burn Key submission MUST be verified as a one-time-use event. A Burn Key that has already been submitted MUST be permanently rejected by the contract.
- Set pool and variant pool balances MUST be updated atomically with the burn release. No intermediate state where funds are released but pool balance is not yet decremented.
- The Last Survivor 1/1 upgrade MUST fire automatically when `cards_remaining_in_variant` reaches 1. This MUST NOT require any manual action from the holder or creator.

---

*PoT Protocol — Architecture v0.1 — Pre-Development*
*For questions, open an issue. For contributions, see CONTRIBUTING.md (forthcoming).*
