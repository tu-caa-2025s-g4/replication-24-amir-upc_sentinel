# 🛢️ Data Source
- [Github repo](https://github.com/JeremieWU23/upgradeable-contracts.git)

# 🆔 Released By
- Yuan Huang et al. [The Sword of Damocles: Upgradeable Smart Contract in Ethereum](https://dl.acm.org/doi/10.1145/3643916.3644426)
- 
# 📅 Published Date
- 2024/06/13

# 📝 Original Description
- A balanced sample of 8,704 UPCs and Non-UPCs.  
- Out of 8,704 contracts, **4,352**  are manually labeled as UPCs and **4,352** are labeled as Non-UPCs.

# ✅ Validated by UPC Sentinel (V2)
Analysis of the 8,704 sampled contracts using UPC Sentinel indicates that **?** are identified as Upgradeability Proxy Contracts (UPCs), with a total of **?** distinct versions as of *2025/04/01*.
- Additionally, UPC Sentinel disagrees with the ground truth labels in **? instances**:
  - **? instances** were classified as UPCs by UPC Sentinel, contrary to the ground truth which labeled them as Non-UPCs.
  - **? instances** were classified as Non-UPCs by UPC Sentinel, while the ground truth labeled them as UPCs.

# 🔍 Discrepancies Between UPC Sentinel and Ground Truth

| **Discrepancy Type**                                   | **Count** | **Description**                                                                 |
|--------------------------------------------------------|:---------:|----------------------------------------------------------------------------------|
| Ground Truth: Non-UPC → UPC Sentinel: ✅ UPC           | ?        | Detected as UPC by UPC Sentinel, but labeled as Non-UPC in the ground truth.     |
| Ground Truth: UPC → UPC Sentinel: ❌ Non-UPC           | ?         | Not detected as UPC by UPC Sentinel, but labeled as UPC in the ground truth.     |
| **Total Discrepancies**                                | **?**    | Total number of mismatches between UPC Sentinel and the ground truth labels.     |

# 📊 Distribution of Upgradeability Reference Designs
| **Reference Design**                                   | **Number of UPCs**                                                |
|--------------------------------------------------------|:-----------------|
| SMUP           | ?       |
| DUP            | ?        |
| ESUP           | ?        |

# 📂 Datasets

The following datasets are included in this directory:

- **Original Dataset.xlsx**  
  Contains the original list of 100 randomly sampled upgradeable smart contracts along with their metadata and version history.

- **UPC Sentinel Verification Result.csv**  
  Contains the validation results produced by UPC Sentinel, including the classification of each contract, detailed information on where the upgrade function is located, and the reasoning behind why a contract is considered a UPC or not.

