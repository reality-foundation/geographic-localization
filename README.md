```mermaid
flowchart TD
    subgraph Global_L0_Network
        L0[Global L0 Cluster (Connects all L1s)]
    end
    subgraph Enforce_Localization
        App[Your Application (Deployed via CLI create-deploy-app-transaction)]
        Restrict>Restrict Data Sharing Gossip/P2P Routes /consensus/data Use Trust Models e.g. TrustNode Distance]
    end
    subgraph Jurisdiction_Specific_L1_Cluster_EU
        subgraph NET_Incentives_2meme_Design
            Stake>Stake NET Collateral --collateral in CLI Boosts Selection Odds SelectActivePeers Scores]
            Rewards>Rewards for Honesty/Performance Earn NET for Blocks/Snapshots Performance Meme High Storage Bonus Virality Meme Reporting Issues]
            Penalties>Penalties for Dishonesty Slash NET on Failed Challenges Drop Trust Eject to Offline]
        end
        L1[L1 Cluster (Nodes in specific region)]
        Node1[Node A (Host IP EU Storage 100GB)]
        Node2[Node B (Host IP EU Storage 200GB)]
    end
    subgraph Prove_Storage_Capacity
        Attest>Report Capacity e.g. 100GB Signed]
        Challenge>Storage/Retrieval Challenges Respond with Signed Hashes]
        Verify>App Verifies via SDK /node/state for Ready Nodes Optional ZK Proof Capacity >= X]
    end
    subgraph Prove_Localization
        Proofs[Signed Snapshots /global-snapshots/app-data Embed Node IDs/Hosts]
        ZK[ZK STARK Proofs e.g. Data in Jurisdiction X]
    end
    L0 -->|L0 Peer Connections Global Sync| L1
    App -->|Deploy to L1 destination /cluster/join| L1
    App -->|Query Peers /node/info /cluster/info Filter by Host IP/Jurisdiction| Restrict
    L1 --> Node1
    L1 --> Node2
    L1 -->|Signed Operations SignatureProof in Signed.scala Verify hasValidSignature| Proofs
    Proofs -->|Optional ZKWasmExecutor| ZK
    L1 -->|Self-Attestation in NodeInfo Signed during Join| Attest
    L1 -->|Cluster Challenges Gossip/Consensus Rounds in RoundData| Challenge
    Challenge -->|Failures Lower Trust Scores SelectActivePeers| Verify
    Verify -->|Historical Audit| Proofs
    Node1 --> Stake
    Node2 --> Stake
    Challenge -->|Pass Earn Rewards| Rewards
    Challenge -->|Fail Slash| Penalties
```
