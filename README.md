```mermaid
graph TD
    subgraph "Global L0 Network"
        L0["Global L0 Cluster\n(Connects all L1s)"]
    end

    subgraph "Jurisdiction-Specific L1 Cluster e.g. EU"
        L1["L1 Cluster\n(Nodes in specific region)"]
        Node1["Node A\n(Host IP: EU, Storage: 100GB)"]
        Node2["Node B\n(Host IP: EU, Storage: 200GB)"]
        L1 --> Node1
        L1 --> Node2
    end

    App["Your Application\n(Deployed via CLI: create-deploy-app-transaction)"]
    App -->|Deploy to L1 destination\n(/cluster/join)| L1

    L0 -->|L0 Peer Connections\n(Global Sync)| L1

    subgraph "Enforce Localization"
        App -->|Query Peers\n(/node/info, /cluster/info)\nFilter by Host IP/Jurisdiction| Restrict["Restrict Data Sharing\n(Gossip/P2P Routes: /consensus/data)\nUse Trust Models (e.g., TrustNode Distance)"]
    end

    subgraph "Prove Localization"
        L1 -->|Signed Operations\n(SignatureProof in Signed.scala)\nVerify: hasValidSignature| Proofs["Signed Snapshots\n(/global-snapshots/app-data)\nEmbed Node IDs/Hosts"]
        Proofs -->|Optional: ZKWasmExecutor| ZK["ZK STARK Proofs\n(e.g., Data in Jurisdiction X)"]
    end

    subgraph "Prove Storage Capacity"
        L1 -->|Self-Attestation in NodeInfo\n(Signed during Join)| Attest["Report Capacity\n(e.g., 100GB, Signed)"]
        L1 -->|Cluster Challenges\n(Gossip/Consensus Rounds in RoundData)| Challenge["Storage/Retrieval Challenges\nRespond with Signed Hashes"]
        Challenge -->|Failures Lower Trust Scores\n(SelectActivePeers)| Verify["App Verifies via SDK\n(/node/state for Ready Nodes)\nOptional ZK Proof: Capacity >= X"]
        Verify -->|Historical Audit| Proofs
    end

    subgraph "NET Incentives 2meme Design"
        Stake["Stake NET Collateral\n(--collateral in CLI)\nBoosts Selection Odds\n(SelectActivePeers Scores)"]
        Node1 --> Stake
        Node2 --> Stake
        Rewards["Rewards for Honesty/Performance\n(Earn NET for Blocks/Snapshots)\nPerformance Meme: High Storage Bonus\nVirality Meme: Reporting Issues"]
        Penalties["Penalties for Dishonesty\n(Slash NET on Failed Challenges)\nDrop Trust, Eject to Offline"]
        Challenge -->|Pass: Earn Rewards| Rewards
        Challenge -->|Fail: Slash| Penalties
    end

    classDef process fill:#f9f,stroke:#333,stroke-width:2px;
    class Restrict,Attest,Challenge,Verify,Stake,Rewards,Penalties process;
