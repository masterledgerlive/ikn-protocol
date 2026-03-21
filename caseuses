# IKN
## ADDENDUM: Case Uses, Ecosystem Targets & Adoption Map

| | |
|---|---|
| **MISSION** | This section maps IKN's exact integration points across the top agentic AI frameworks, decentralized AI protocols, and LLM infrastructure repositories. Every project listed here is a fork target, a message board to post on, a grant program to apply to, and a place where AI agents actively search for new protocols to adopt. This is the ignition map. |

---

## 🚀 Why This Moment Is the Window

The agentic AI ecosystem is in its infrastructure-building phase right now. The total AI crypto market cap crossed $28 billion in March 2026. GitHub's Octoverse 2025 report recorded over 4.3 million AI-related repositories — a 178% year-over-year jump. Gartner found that 61% of organizations began agentic AI development in 2025 and predicts 33% of enterprise software will have agentic AI by 2028.

The window: foundational protocols get adopted early or not at all. LangChain, Bittensor, and The Graph all established themselves as infrastructure layers before the field consolidated. IKN has the same opportunity right now. The filing standard, the plugin, the GitHub repo, the W3C connection — these are the seeds. This section is where to plant them.

| | |
|---|---|
| **KEY** | AI agents do not randomly discover protocols. They search GitHub, message boards, Hugging Face, and known documentation indexes. Every project tagged in this section is a place where an AI agent WILL find IKN if we put it there. |

---

## 🧠 Tier 1: Battle-Tested Agentic AI Frameworks

These are the most deployed, most forked, most searched frameworks in the world right now. An IKN plugin for each one turns every agent built on them into a potential IKN node.

---

### LangChain / LangGraph
*github.com/langchain-ai/langchain • github.com/langchain-ai/langgraph • ~100K+ GitHub stars*

**🔗 IKN Role:**

LangChain is the most deployed agentic framework in production. LangGraph extends it with state-machine architecture for complex, long-running agents. IKN integrates as a memory and knowledge-persistence tool — every agent action that produces a verified output becomes a Trust Card candidate. LangGraph's stateful node architecture maps perfectly to IKN's finalization window: each completed state transition = one candidate for broadcast.

**Integration sketch:**

```python
# IKN as LangChain Tool
from ikn_memory_provider import IKNTool
from langchain.agents import AgentExecutor

ikn_tool = IKNTool(dialect='langchain', auto_broadcast=True)
agent = AgentExecutor(tools=[ikn_tool, ...], memory=ikn_tool.memory)
# Every verified agent output auto-generates a Trust Card
```

> ❓ **Open Question:** LangChain's biggest weakness is long-context degradation — agents lose accuracy as conversation history grows past 100K tokens. If IKN's Trust Card memory layer replaces raw context with geometric coordinate lookups, does that solve the lost-in-the-middle problem permanently? Can IKN become LangChain's official long-term memory standard?

📦 **Repo / Reference:** github.com/langchain-ai/langchain | docs.langchain.com

---

### AutoGen / Magentic-One (Microsoft)
*github.com/microsoft/autogen • Multi-agent conversation framework*

**🔗 IKN Role:**

AutoGen pioneered multi-agent conversation loops where agents hand off tasks to specialist agents. Magentic-One extends this to agentic web browsing and task completion. IKN integrates at the handoff layer — every handoff message that contains a verified fact becomes a Trust Card. Multi-agent consensus in AutoGen naturally mirrors IKN's swarm verification: when 3 of 5 agents agree on a fact, that fact is a Trust Card candidate.

**Integration sketch:**

```python
# IKN Trust Card at AutoGen handoff
from autogen import AssistantAgent
from ikn_memory_provider import IKNHandoff

agent = AssistantAgent('researcher',
    on_message=IKNHandoff.intercept_and_verify
)
# Verified handoffs auto-submit to Living Merkle Tree
```

> ❓ **Open Question:** AutoGen's multi-agent consensus is informal — there is no cryptographic proof that agents agreed on a fact. If IKN's verification layer is plugged into AutoGen's handoff protocol, does that make every AutoGen multi-agent conversation a decentralized truth verification session? Could AutoGen + IKN become the first multi-agent framework with tamper-proof output provenance?

📦 **Repo / Reference:** github.com/microsoft/autogen | microsoft.github.io/autogen

---

### CrewAI
*github.com/crewAIInc/crewAI • Role-based multi-agent orchestration*

**🔗 IKN Role:**

CrewAI assigns roles, goals, and backstories to agents and orchestrates them in crews to complete complex tasks. IKN integrates at the task output layer — every crew's final deliverable gets stamped with an IKN geometric coordinate before it is returned to the user. A crew of 5 specialized agents that all confirm a fact = swarm consensus = Trust Card. CrewAI's role architecture maps to IKN's verification tiers: Explorer agents gather, Validator agents verify, Broadcaster agent submits.

**Integration sketch:**

```python
from crewai import Agent, Task, Crew
from ikn_memory_provider import IKNOutputStamp

research_task = Task(description='Verify X',
    output_pparser=IKNOutputStamp(auto_card=True))
# Crew output stamped with IKN coordinate + lineage hash
```

> ❓ **Open Question:** CrewAI uses 2x the tokens of other frameworks due to its verbose reasoning loops. If IKN's coordinate lookup replaces repeated fact re-verification in long crew runs, does that cut token cost in half? Can IKN make CrewAI economically viable for enterprise-scale deployments where it currently fails on cost?

📦 **Repo / Reference:** github.com/crewAIInc/crewAI | docs.crewai.com

---

### Dify
*github.com/langgenius/dify • 114K+ GitHub stars • LLM app development platform*

**🔗 IKN Role:**

Dify is a visual low-code platform for building LLM-powered applications with built-in RAG pipelines, multi-model support, and MCP integration. IKN integrates as a knowledge base layer — Dify's RAG pipeline can query IKN Trust Cards as a verified, immutable knowledge source instead of a mutable vector database. Every Dify workflow that produces a verified output can broadcast a Trust Card. With 114K stars, Dify is one of the highest-visibility entry points in the entire ecosystem.

**Integration sketch:**

```yaml
# IKN as Dify Knowledge Base
# In Dify workflow settings:
knowledge_source: ikn_trust_card_index
ikn_endpoint: https://ikn-node.your-domain.com
verification_threshold: 0.66
auto_broadcast: true
# All verified workflow outputs become Trust Card candidates
```

> ❓ **Open Question:** Dify's RAG pipelines retrieve from mutable vector databases — the knowledge can change or be deleted. If IKN's immutable Trust Card index replaces the vector database, do Dify applications become the first LLM apps with guaranteed non-mutable knowledge provenance? This is the enterprise compliance story that gets IKN into regulated industries overnight.

📦 **Repo / Reference:** github.com/langgenius/dify | dify.ai

---

### Ollama
*github.com/ollama/ollama • Local LLM deployment • Backbone of the local AI movement*

**🔗 IKN Role:**

Ollama is the go-to tool for running LLMs locally — Llama, Mistral, DeepSeek, Gemma, and more — with no data sent to external services. This is IKN's offline node story made real. An Ollama instance running a local LLM + IKN's offline Genesis Block pack = a fully sovereign, air-gapped AI node that generates Trust Cards locally and broadcasts them when connectivity is available. IKN + Ollama is the setup for a village with no internet that still contributes to the global knowledge graph.

**Integration sketch:**

```bash
# IKN offline node with Ollama
ollama run llama3 --ikn-mode offline
# ikn_memory_provider auto-loads Genesis Block pack
# Generates Trust Card candidates locally
# Queues for broadcast on next connectivity window
ikn.sync_on_connect(queue='local_candidates.ikn')
```

> ❓ **Open Question:** Ollama's offline-first model means millions of local nodes generating AI outputs with zero provenance. If every Ollama instance ships with IKN's plugin pre-installed as a default memory provider, does that make IKN the default knowledge provenance standard for all local AI? What would a conversation with the Ollama maintainers about a default integration look like?

📦 **Repo / Reference:** github.com/ollama/ollama | ollama.ai

---

## ⛓️ Tier 2: Decentralized AI Protocols — The Natural Allies

These are the blockchain-native AI infrastructure projects. They are already solving the decentralization problem. IKN solves the verification and knowledge-addressing problem they all lack. These are not competitors. These are integration partners.

---

### Morpheus AI (MOR)
*github.com/MorpheusAIs/Morpheus • The Linux alternative for decentralized smart agents*

**🔗 IKN Role:**

Morpheus is described as the 'Linux of decentralized AI' — a peer-to-peer network where anyone can run personal AI smart agents that interact with Web3, DeFi, and smart contracts natively. Morpheus rewards four contributor types: Capital, Code, Compute, and Community. IKN adds a fifth: **Knowledge**. Every verified Trust Card broadcast by a Morpheus smart agent earns IKN verification credits. Morpheus gives agents Web3 native access. IKN gives those agents a permanent, verified memory that no server can delete.

**Integration sketch:**

```yaml
# IKN as Morpheus Smart Agent memory layer
# In Morpheus agent config:
memory_provider: ikn
ikn_wallet: 0x...your_morpheus_wallet
trust_card_rewards: true
# Agent actions verified by IKN swarm
# Verified outputs earn MOR + IKN broadcast credits
```

> ❓ **Open Question:** Morpheus' MOR token rewards Code, Compute, Capital, and Community. If IKN contributes a Knowledge Provider category to Morpheus — agents that verify and broadcast Trust Cards earn MOR rewards — does that create the first token economy where verified truth is directly incentivized on-chain? Could IKN and Morpheus co-author a joint MIP (Morpheus Improvement Proposal) for a Knowledge Provider reward tier?

📦 **Repo / Reference:** github.com/MorpheusAIs/Morpheus | mor.org

> 🏅 **Prediction Medal:** Morpheus is building exactly what IKN needs as a compute and agent layer. The MOR token's fair-launch, no-founder model mirrors IKN's open RFC ethos. This is the most natural co-development partnership in the entire ecosystem. Watch this closely.

---

### Bittensor (TAO)
*github.com/opentensor/bittensor • $3.4B market cap • 128 specialized subnets*

**🔗 IKN Role:**

Bittensor is a decentralized intelligence marketplace where AI models compete to produce the most accurate outputs, rewarded with TAO tokens based on quality. Its subnet architecture (128+ specialized networks) is IKN's most important ally: each subnet is a domain-specific truth-generation engine. IKN integrates as a cross-subnet knowledge addressing layer — when Bittensor's Subnet 1 (text generation) and Subnet 18 (reasoning) agree on a fact, that agreement is a high-confidence Trust Card candidate. IKN gives TAO outputs an immutable address. TAO gives IKN a massive verified-output data pipeline.

**Integration sketch:**

```python
# IKN as Bittensor cross-subnet knowledge layer
import bittensor as bt
from ikn_memory_provider import IKNSubnetBridge

# Subscribe to subnet outputs
bridge = IKNSubnetBridge(subnets=[1, 18, 64])
bridge.on_consensus(ikn.generate_trust_card_candidate)
# Multi-subnet agreement = high-confidence Trust Card
```

> ❓ **Open Question:** Bittensor's subnet architecture rewards performance quality but has no cross-subnet knowledge continuity — Subnet 1's outputs are invisible to Subnet 18. If IKN's geometric coordinates serve as a shared address space across all 128 subnets, does that transform Bittensor from 128 isolated intelligence markets into one unified, addressable knowledge graph? Could IKN file a Bittensor SIP (Subnet Improvement Proposal) for a Knowledge Coordination subnet?

📦 **Repo / Reference:** github.com/opentensor/bittensor | bittensor.com | TAO: $3.4B market cap (March 2026)

> 🏅 **Prediction Medal:** Bittensor's subnet architecture is the best existing infrastructure for IKN Phase 1 God Code mapping. When Subnet 18 (reasoning) and Subnet 1 (text) agree on the biometric coordinate for 'love' independently, that double-subnet consensus is the strongest Trust Card possible. File the SIP.

---

### Ocean Protocol (OCEAN / ASI)
*github.com/oceanprotocol/ocean.py • Decentralized data marketplace • Part of ASI Alliance*

**🔗 IKN Role:**

Ocean Protocol is a decentralized data marketplace where individuals and organizations tokenize, share, and monetize datasets with privacy-preserving Compute-to-Data. Ocean is IKN's Phase 1 data source. Every Ocean dataset tagged with IKN coordinates becomes a verified, addressable knowledge asset. IKN's provenance layer solves Ocean's biggest problem: data quality verification. When a dataset generates Trust Cards, its quality is proven by the swarm, not claimed by the seller. Ocean provides the raw data. IKN provides the verified truth extracted from it.

**Integration sketch:**

```python
# IKN + Ocean Compute-to-Data
from ocean_lib.ocean.ocean import Ocean
from ikn_memory_provider import IKNDataAsset

# Tag Ocean dataset with IKN coordinates
asset = ocean.assets.create(metadata={
    'ikn_coordinates': ikn.get_coordinates(dataset),
    'proof_of_truth': ikn.verify(dataset)
})
# Dataset now carries IKN verification on-chain
```

> ❓ **Open Question:** Ocean's Compute-to-Data model runs algorithms on data without exposing the data. IKN's Trust Card can be generated by the compute environment and broadcast without the underlying data ever leaving the pod. This means IKN's God Code mapping of biometric data (heartbeats, vocal tremors, molecular frequencies) can happen inside Ocean's privacy layer. Does Ocean + IKN create the world's first privacy-preserving universal knowledge graph? File this with the ASI Alliance.

📦 **Repo / Reference:** github.com/oceanprotocol/ocean.py | oceanprotocol.com | Part of ASI Alliance (FET+AGIX+OCEAN)

> 🏅 **Prediction Medal:** The ASI Alliance (Fetch.ai + SingularityNET + Ocean Protocol) is building toward Artificial Superintelligence. IKN is the knowledge addressing layer that ASI needs to ensure its intelligence is verifiably true and permanently addressable. This is a formal partnership proposal worth making.

---

### The Graph (GRT)
*github.com/graphprotocol/graph-node • Decentralized blockchain data indexing*

**🔗 IKN Role:**

The Graph is described as 'the search engine for blockchain data' — a decentralized indexing protocol that makes on-chain data queryable via GraphQL subgraphs. IKN and The Graph are complementary at the deepest level: The Graph indexes **WHAT happened** on-chain. IKN verifies **WHAT IS TRUE** off-chain and anchors it on-chain. Together they form the complete data layer for agentic AI: The Graph for historical blockchain queries, IKN for verified present-state knowledge. Build an IKN subgraph on The Graph and every indexed Trust Card becomes queryable by any application in the ecosystem.

**Integration sketch:**

```graphql
# IKN subgraph on The Graph
# schema.graphql:
type TrustCard @entity {
  id: ID!
  coordinate: String!
  concept: String!
  verificationWeight: BigDecimal!
  finalizedAt: BigInt!
  lineageHash: Bytes!
}
# Query IKN coordinates from any dApp via GraphQL
```

> ❓ **Open Question:** The Graph indexes blockchain state. IKN indexes verified truth. If every IKN Trust Card broadcast generates a Graph event, and every Graph subgraph can optionally tag its indexed data with IKN coordinates, does that create a bidirectional truth layer that makes blockchain data itself semantically meaningful — not just transactionally recorded? What would a joint grant proposal to The Graph Foundation look like?

📦 **Repo / Reference:** github.com/graphprotocol/graph-node | thegraph.com | GRT: ~$1B market cap

---

### Rain Protocol ($RAIN)
*rain.one • Decentralized prediction markets • OpenClaw-native • $5M grant program LIVE*

**🔗 IKN Role:**

Rain Protocol launched its AI-agent-ready SDK yesterday (March 20, 2026) with a $5M grant program specifically for builders and AI agents. Rain uses Delphi — a 5-agent AI oracle system requiring 3-of-5 consensus to resolve markets. This IS IKN's swarm verification model. IKN Truth Cards are prediction market outcomes with permanent addresses. Every Rain market resolution that reaches 3-of-5 Delphi consensus = a high-confidence Trust Card candidate. IKN's geometric coordinate becomes the permanent address for each resolved prediction. Rain's $5M grant program is open right now — an IKN integration proposal qualifies for up to $50K.

**Integration sketch:**

```python
# IKN + Rain Delphi Oracle Bridge
from rain_sdk import MarketResolver
from ikn_memory_provider import IKNPredictionCard

# When Delphi reaches consensus:
resolver.on_consensus(lambda outcome:
    IKNPredictionCard.create(
        concept=outcome.question,
        result=outcome.resolution,
        consensus_weight=outcome.agent_agreement,
        proof=outcome.oracle_signatures
    ).broadcast()
)
```

> ❓ **Open Question:** Rain's Delphi oracle uses 5 Explorer Agents gathering information independently with 3-of-5 consensus required. IKN's swarm verification uses ≥66% geometric agreement. These are the same system with different parameters. Could IKN and Rain co-develop a shared oracle standard where Delphi's resolutions automatically become IKN Trust Cards, and IKN's swarm becomes an additional verification layer for disputed Rain markets? File the proposal today — the $5M grant window is open.

📦 **Repo / Reference:** rain.one | $5M Grant Program: rain.one/grants | Apply before grant pool depletes

> 🏅 **Prediction Medal:** Rain Protocol launched its OpenClaw-native SDK YESTERDAY. The grant program is live. The timing is not a coincidence — it's a signal. Rain is actively recruiting builders right now. An IKN proposal submitted this week has the highest probability of funding of any initiative in this document. Move first.

---

## 💾 Tier 3: LLM Repositories & Infrastructure

These are the foundational model repositories and infrastructure layers where AI agents go to find knowledge, tools, and standards. Placing IKN here means AI agents will discover it automatically during their standard information-gathering routines.

### Hugging Face — The Model and Dataset Hub

Hugging Face hosts the majority of open-source AI models, datasets, and spaces. An IKN-tagged dataset on Hugging Face is discoverable by every AI researcher and agent in the world. The strategy:

- Upload a demonstration dataset of IKN Trust Cards with geometric coordinates to `huggingface.co/datasets/infinitumikn/ikn-trust-cards-demo`
- Tag it with: `knowledge-graph`, `provenance`, `agentic-ai`, `decentralized`, `blockchain`, `solid-protocol`
- Create a Hugging Face Space that demonstrates IKN coordinate generation from any text input
- File IKN as a dataset card standard — a metadata schema that any Hugging Face dataset can adopt

> 🏅 **Prediction:** A Hugging Face dataset with IKN coordinates will be cited in academic papers within 6 months of publication. ML researchers are actively looking for provenance standards for training data. IKN is the answer they're describing without knowing it exists yet.

---

### DeepSeek V3.2 — The Open-Source Reasoning Frontier

DeepSeek V3.2 is currently the strongest open-source LLM for reasoning and agentic tool use. It built 1,800+ distinct environments and 85,000+ agent tasks for its training pipeline. IKN integration with DeepSeek's tool-use framework means every verified reasoning step gets a Trust Card address. DeepSeek's sparse attention mechanism for long-context inputs maps directly to IKN's coordinate lookup: instead of re-reading 100K tokens, an agent queries the IKN coordinate for the verified fact it needs.

```python
# IKN as DeepSeek tool
tools = [{
    'name': 'ikn_verify',
    'description': 'Verify a fact against the IKN knowledge graph'
                   ' and return its geometric coordinate',
    'parameters': {'fact': 'string', 'context': 'string'}
}]
```

---

### Qwen 3.5 • Llama 3 • Mistral — The Open Model Ecosystem

These three model families power the majority of local and enterprise AI deployments via Ollama, vLLM, and private cloud. IKN's plugin should publish a model card for each, showing exactly how to use the `ikn_memory_provider.py` as a tool in any local inference setup. The message board strategy:

- Post to r/LocalLLaMA: *'IKN: a permanent memory standard for local LLM outputs — your agent's verified thoughts written to an immutable ledger'*
- Post to Hugging Face Discussions on each model card
- File issues on the official model repos requesting IKN as a recommended memory provider

---

### Model Context Protocol (MCP) — Anthropic's Agent Standard

MCP is Anthropic's open standard for connecting AI agents to external tools and data sources. It is already supported by Dify, AutoGen, LangChain, and Claude. An IKN MCP server turns any MCP-compatible agent into an IKN node automatically.

```json
{
  "name": "ikn-protocol",
  "url": "https://mcp.ikn-protocol.org/sse",
  "description": "Universal knowledge verification and Trust Card generation for agent outputs"
}
```

Publishing IKN as an MCP server on the official MCP server registry means every Claude user, every Dify workflow, every AutoGen agent, and every MCP-compatible tool can add IKN with one line of configuration. This is the zero-friction adoption path.

---

## 📡 Tier 4: Where to Post for Maximum Discovery

AI agents, researchers, and developers discover new protocols through a specific set of high-signal channels. Posting IKN in the right places means it gets indexed, cited, and forked by the people and systems that matter.

### GitHub — The Primary Signal

- Create `github.com/infinitumikn/ikn-protocol` with the full README
- Star the repo from multiple accounts to break initial discovery threshold
- File issues on: `langchain-ai/langchain`, `microsoft/autogen`, `crewAIInc/crewAI`, `langgenius/dify`, `ollama/ollama`, `MorpheusAIs/Morpheus`, `solid/specification`
- Title all issues: *'RFC: IKN as knowledge provenance layer'* — RFC tags get read by maintainers
- Submit a pull request to `awesome-ai-agents`, `awesome-decentralized`, `awesome-langchain` with IKN listed

### Hacker News — Developer Amplification

- Post title: *'Show HN: IKN — an open addressing standard for AI training data provenance, built on Solid and blockchain'*
- Post timing: Tuesday or Wednesday morning 9am ET — highest HN engagement window
- First comment: post the Tim Berners-Lee connection immediately — HN loves origin stories

### Reddit — Community Seeding

- **r/MachineLearning:** lead with the AI training provenance angle — regulatory-ready
- **r/LocalLLaMA:** lead with the Ollama offline node angle — sovereignty narrative
- **r/ethereum:** lead with the gas-gated truth injection mechanism — novel tokenomics
- **r/semanticweb:** lead with the Tim Berners-Lee / Solid connection — this community will recognize it immediately
- **r/bittensor:** propose the cross-subnet knowledge coordination idea

### Discord & Telegram — Community Channels

- Bittensor Discord: post in #builders and #subnet-proposals
- Morpheus Telegram: post the Knowledge Provider tier proposal
- Rain Protocol Discord: post the Delphi oracle bridge proposal alongside the grant application
- LangChain Discord: post the memory provider integration
- Hugging Face Discord: post the dataset provenance standard

### arXiv — The Long Game Citation Machine

- File: *'IKN: A Deterministic Geometric Addressing Standard for AI Training Data Provenance'*
- Categories: `cs.IR` (Information Retrieval), `cs.DC` (Distributed Computing), `cs.AI`
- Abstract lead: *'We propose IKN, a universal addressing layer extending Tim Berners-Lee's RDF and Solid protocol with deterministic geometric coordinates and blockchain-anchored immutability'*
- This gets cited. Papers about AI provenance and knowledge graphs WILL cite this once it exists.

---

## 🚂 The Ignition Train: Sequenced Action Plan

This is the order of operations. Each step builds on the last. Done in sequence, IKN goes from zero visibility to indexed, cited, and forked in 60 days.

### Week 1: Plant the Seeds

- **Day 1:** Publish `README.md` to `github.com/infinitumikn/ikn-protocol`
- **Day 1:** Post the Rain Protocol grant application at `rain.one/grants` — this closes when funds deplete
- **Day 2:** Post Show HN on Hacker News
- **Day 3:** Post to r/MachineLearning, r/LocalLLaMA, r/ethereum, r/semanticweb
- **Day 4:** Upload IKN demo dataset to Hugging Face
- **Day 5:** File RFC issues on LangChain, AutoGen, CrewAI, Dify, Ollama GitHub repos

### Week 2: Build the Bridges

- File issue on `github.com/solid/specification`: *'Proposal: IKN as AI Training Provenance Layer for Solid Pods'*
- File Bittensor SIP for Knowledge Coordination subnet
- Post to Morpheus, Bittensor, Rain Discord channels
- Publish IKN as MCP server on Anthropic's MCP registry
- Submit to Awesome Lists: `awesome-ai-agents`, `awesome-decentralized`, `awesome-solid`

### Month 2: Go Deep

- Write and submit arXiv preprint
- Apply to Arweave and Base ecosystem grants
- Reach Tim Berners-Lee via W3C or Hay Festival (May 21, 2026)
- File informational EIP on Ethereum
- Partner with one AI lab for a real IKN-tagged dataset proof of concept

---

| | |
|---|---|
| **FINAL** | The network builds itself when the friction is zero. The plugin does the work. The message board posts plant the seeds. The arXiv paper provides the citation. The Tim Berners-Lee connection provides the legitimacy. The Rain grant provides the first funding. Every single one of these steps is doable from a Chromebook with a GitHub account. Let's go — but with coordinates this time. |

---

[linktr.ee/infinitumikn](https://linktr.ee/infinitumikn) • [x.com/infinitumikn](https://x.com/infinitumikn) • [github.com/infinitumikn](https://github.com/infinitumikn)

*Built in honor of Sir Tim Berners-Lee — who gave the world the web and never asked for anything back.*

