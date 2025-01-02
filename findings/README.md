# RQ1 Findings Sheet
This document provides a description of the columns in the **RQ1 Findings** sheet. The sheet contains labels and predictions for UPC identification tasks on the GE ground truth containting 3,177 collected UPCs.

### `contract_address`
- **Description:** The unique Ethereum contract address.
### `is-upc-groundtruth`
- **Description:** The ground truth UPC label provided by Ebrahimi et al. All 3,177 instances are UPCs.
### `is-upc-upcsentinel`
- **Description:** Prediction of UPC Sentinel for the UPC identification task.
### `is-proxy-upcsentinel`
- **Description:** Prediction of UPC Sentinel for the proxy identification task.
### `implementation-contracts`
- **Description:** The complete list of implementation contract addresses collected as of Sept. 2022.


# RQ2 & RQ3 Findings Sheet
This document provides a description of the columns in the **RQ2 & RQ3 Findings** sheet. The sheet contains labels and predictions for proxy and UPC identification tasks in Ethereum smart contracts.

## Column Descriptions

### `contract_address`
- **Description:** The unique Ethereum contract address.

### `is-proxy-groundtruth-bodell (GB1) (original label by bodell III et al)`
- **Description:** The original proxy label (i.e., whether it is a proxy or non-proxy) provided by Bodell III et al. [1].

### `is-proxy-groundtruth-bodell (GB2) (refined label by ebrahimi et al)`
- **Description:** The refined proxy label provided by Ebrahimi et al. [2].
- **Note:** Please refer to the manuscript for more details.

### `is-active-proxy`
- **Description:** Indicates if the proxy is active or inactive.

### `is-proxy-uschunt`
- **Description:** Prediction of USCHUNT for the proxy identification task, based on the USCHUNT replication package.

### `is-proxy-upcsentinel`
- **Description:** Prediction of UPC Sentinel for the proxy identification task.

### `is-upc-groundtruth-bodell (GB1) (original label by bodell III et al)`
- **Description:** The original UPC label (i.e., whether it is a UPC or non-UPC) provided by Bodell III et al. [1].

### `is-upc-groundtruth-bodell (GB3) (refined label by ebrahimi et al)`
- **Description:** The refined UPC label provided by Ebrahimi et al. [2].
- **Note:** Please refer to the manuscript for more details.

### `is-upc-uschunt`
- **Description:** Prediction of USCHUNT for the UPC identification task, based on the USCHUNT replication package.

### `is-upc-upcsentinel`
- **Description:** Prediction of UPC Sentinel for the UPC identification task, based on the USCHUNT replication package.

## References
[1] Bodell III, William E., Sajad Meisami, and Yue Duan. "Proxy hunting: understanding and characterizing proxy-based upgradeable smart contracts in blockchains." 32nd USENIX Security Symposium (USENIX Security 23). 2023.

[2] Ebrahimi, Amir & Adams, Bram & Oliva, Gustavo & Hassan, Ahmed E.. (2023). UPC Sentinel: An Accurate Approach for Detecting Upgradeability Proxy Contracts in Ethereum. 10.13140/RG.2.2.34439.16808. 
