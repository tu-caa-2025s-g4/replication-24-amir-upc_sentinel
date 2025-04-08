# 📊 Data Source
- [Zenodo Record](https://zenodo.org/records/7734661)

# 🆔 Released By
- Anonymous

# 📅 Published Date
- 2023/03/14

# 📝 Original Description
- We have randomly sampled 100 upgradeable contracts and traced their upgrades and versions.  
- Out of 100 contracts, **32 were upgraded**, resulting in **76 overall versions**.

# ✅ Validated by UPC Sentinel (V2)
Analysis of the 100 sampled contracts indicates that **37** are identified as Upgradeability Proxy Contracts (UPCs), with a total of **82** distinct versions as of *2025/04/01*.
- Additionally, UPC Sentinel disagrees with the ground truth labels in **21 instances**:
  - **13 instances** were classified as UPCs by UPC Sentinel, contrary to the ground truth which labeled them as Non-UPCs.
  - **8 instances** were classified as Non-UPCs by UPC Sentinel, while the ground truth labeled them as UPCs.

# 🔍 Discrepancies Between UPC Sentinel and Ground Truth

| **Discrepancy Type**                                   | **Count** | **Description**                                                                 |
|--------------------------------------------------------|:---------:|----------------------------------------------------------------------------------|
| Ground Truth: Non-UPC → UPC Sentinel: ✅ UPC           | 13        | Detected as UPC by UPC Sentinel, but labeled as Non-UPC in the ground truth.     |
| Ground Truth: UPC → UPC Sentinel: ❌ Non-UPC           | 8         | Not detected as UPC by UPC Sentinel, but labeled as UPC in the ground truth.     |
| **Total Discrepancies**                                | **21**    | Total number of mismatches between UPC Sentinel and the ground truth labels.     |

# 📂 Datasets

The following datasets are included in this directory:

- **Original Dataset.xlsx**  
  Contains the original list of 100 randomly sampled upgradeable smart contracts along with their metadata and version history.

- **UPC Sentinel Verification Result.csv**  
  Contains the validation results produced by UPC Sentinel, including the classification of each contract, detailed information on where the upgrade function is located, and the reasoning behind why a contract is considered a UPC or not.

