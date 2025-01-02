
# GB - 920 UPCs & Non-UPCs.csv
This document provides a description of the columns in the **GB - 920 UPCs & Non-UPCs.csv** sheet. 
The sheet contains the original ground truth labels provided by Bodell III et al.'s replication package, as well as the refined labels for instances where the original ground truth was incorrect and subsequently updated during our study. For additional details, please consult the accompanying manuscript or relevant references.

## Column Descriptions

### `contract_address`
- **Description:** The unique Ethereum contract address.

### `is-proxy-groundtruth-bodell (GB1) (original label by bodell III et al)`
- **Description:** The original proxy label (i.e., whether it is a proxy or non-proxy) provided by Bodell III et al.

### `is-proxy-groundtruth-bodell (GB2) (refined label by ebrahimi et al)`
- **Description:** The refined proxy label provided by Ebrahimi et al.
- **Note:** Please refer to the manuscript for more details.

### `is-upc-groundtruth-bodell (GB1) (original label by bodell III et al)`
- **Description:** The original UPC label (i.e., whether it is a UPC or non-UPC) provided by Bodell III et al.

### `is-upc-groundtruth-bodell (GB3) (refined label by ebrahimi et al)`
- **Description:** The refined UPC label provided by Ebrahimi et al.
- **Note:** Please refer to the manuscript for more details.
  
# GE - 3177 UPCs.csv
This document provides a description of the columns in the **GE - 3177 UPCs.csv** sheet. 
The sheet contains 3,177 upgradeability proxy contracts (UPCs) collected during our study from Etherscan. It serves as an additional ground truth for evaluating UPC detection methods.
