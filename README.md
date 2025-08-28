# geographic-localization


graph TD
    subgraph "Global L0 Network"
        L0[Global L0 Cluster<br/>(Connects all L1s)]
    end

    subgraph "Jurisdiction-Specific L1 Cluster (e.g., EU)"
        L1[L1 Cluster<br/>(Nodes in specific region)]
        Node1[Node A<br/>(Host IP: EU, Storage: 100GB)]
        Node2[Node B<br/>(Host IP: EU, Storage: 200GB)]
        L1 --> Node1
        L1 --> Node2
    end

    App[Your Application<br/>(Deployed via CLI: create-deploy-app-transaction)]
    App -->|Deploy to L1 destination<br/>(/cluster/join)| L1

    L0 -->|L0 Peer Connections<br/>(Global Sync)| L1

    subgraph "Enforce Localization"
        App -->|Query Peers<br/>(/node/info, /cluster/info)<br/>Filter by Host IP/Jurisdiction| Restrict[Restrict Data Sharing<br/>(Gossip/P2P Routes: /consensus/data)<br/>Use Trust Models (e.g., TrustNode Distance)]
    end

    subgraph "Prove Localization"
        L1 -->|Signed Operations<br/>(SignatureProof in Signed.scala)<br/>Verify: hasValidSignature| Proofs[Signed Snapshots<br/>(/global-snapshots/app-data)<br/>Embed Node IDs/Hosts]
        Proofs -->|Optional: ZKWasmExecutor| ZK[ZK STARK Proofs<br/>(e.g., "Data in Jurisdiction X")]
    end

    subgraph "Prove Storage Capacity"
        L1 -->|Self-Attestation in NodeInfo<br/>(Signed during Join)| Attest[Report Capacity<br/>(e.g., 100GB, Signed)]
        L1 -->|Cluster Challenges<br/>(Gossip/Consensus Rounds in RoundData)| Challenge[Storage/Retrieval Challenges<br/>Respond with Signed Hashes]
        Challenge -->|Failures Lower Trust Scores<br/>(SelectActivePeers)| Verify[App Verifies via SDK<br/>(/node/state for "Ready" Nodes)<br/>Optional ZK Proof: "Capacity >= X"]
        Verify -->|Historical Audit| Proofs
    end

    subgraph "NET Incentives (2meme Design)"
        Stake[Stake NET Collateral<br/>(--collateral in CLI)<br/>Boosts Selection Odds<br/>(SelectActivePeers Scores)]
        Node1 --> Stake
        Node2 --> Stake
        Rewards[Rewards for Honesty/Performance<br/>(Earn NET for Blocks/Snapshots)<br/>Performance Meme: High Storage Bonus<br/>Virality Meme: Reporting Issues]
        Penalties[Penalties for Dishonesty<br/>(Slash NET on Failed Challenges)<br/>Drop Trust, Eject to "Offline"]
        Challenge -->|Pass: Earn Rewards| Rewards
        Challenge -->|Fail: Slash| Penalties
    end

    classDef process fill:#f9f,stroke:#333,stroke-width:2px;
    class Restrict,Attest,Challenge,Verify,Stake,Rewards,Penalties process;
I got another syntax error. I am pasting this into a markdown file in github FYI

Mermaid Syntax Error
View diagram source
graph TD
    subgraph "Global L0 Network"
        L0[Global L0 Cluster<br/>(Connects all L1s)]
    end

    subgraph "Jurisdiction-Specific L1 Cluster (e.g., EU)"
        L1[L1 Cluster<br/>(Nodes in specific region)]
        Node1[Node A<br/>(Host IP: EU, Storage: 100GB)]
        Node2[Node B<br/>(Host IP: EU, Storage: 200GB)]
        L1 --> Node1
        L1 --> Node2
    end

    App[Your Application<br/>(Deployed via CLI: create-deploy-app-transaction)]
    App -->|Deploy to L1 destination<br/>(/cluster/join)| L1

    L0 -->|L0 Peer Connections<br/>(Global Sync)| L1

    subgraph "Enforce Localization"
        App -->|Query Peers<br/>(/node/info, /cluster/info)<br/>Filter by Host IP/Jurisdiction| Restrict[Restrict Data Sharing<br/>(Gossip/P2P Routes: /consensus/data)<br/>Use Trust Models (e.g., TrustNode Distance)]
    end

    subgraph "Prove Localization"
        L1 -->|Signed Operations<br/>(SignatureProof in Signed.scala)<br/>Verify: hasValidSignature| Proofs[Signed Snapshots<br/>(/global-snapshots/app-data)<br/>Embed Node IDs/Hosts]
        Proofs -->|Optional: ZKWasmExecutor| ZK[ZK STARK Proofs<br/>(e.g., Data in Jurisdiction X)]
    end

    subgraph "Prove Storage Capacity"
        L1 -->|Self-Attestation in NodeInfo<br/>(Signed during Join)| Attest[Report Capacity<br/>(e.g., 100GB, Signed)]
        L1 -->|Cluster Challenges<br/>(Gossip/Consensus Rounds in RoundData)| Challenge[Storage/Retrieval Challenges<br/>Respond with Signed Hashes]
        Challenge -->|Failures Lower Trust Scores<br/>(SelectActivePeers)| Verify[App Verifies via SDK<br/>(/node/state for Ready Nodes)<br/>Optional ZK Proof: Capacity >= X]
        Verify -->|Historical Audit| Proofs
    end

    subgraph "NET Incentives (2meme Design)"
        Stake[Stake NET Collateral<br/>(--collateral in CLI)<br/>Boosts Selection Odds<br/>(SelectActivePeers Scores)]
        Node1 --> Stake
        Node2 --> Stake
        Rewards[Rewards for Honesty/Performance<br/>(Earn NET for Blocks/Snapshots)<br/>Performance Meme: High Storage Bonus<br/>Virality Meme: Reporting Issues]
        Penalties[Penalties for Dishonesty<br/>(Slash NET on Failed Challenges)<br/>Drop Trust, Eject to Offline]
        Challenge -->|Pass: Earn Rewards| Rewards
        Challenge -->|Fail: Slash| Penalties
    end

    classDef process fill:#f9f,stroke:#333,stroke-width:2px;
    class Restrict,Attest,Challenge,Verify,Stake,Rewards,Penalties process;
