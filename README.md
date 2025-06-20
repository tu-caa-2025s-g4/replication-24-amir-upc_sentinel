# UPC Sentinel
We now introduce the UPC Sentinel algorithm, which detects upgradeability proxy contracts (UPCs) through a three-layered approach. The input to UPC Sentinel is a list of smart contract addresses. 

Following Figure illustrates the architecture of UPC Sentinel, comprising three distinct layers:  
1. **Proxy Contract Detector**: Determines if a given contract operates as a proxy.
2. **Upgradeability Detector**: Examines whether an identified proxy contract is specifically tailored for upgradeability purposes.
3. **Upgradeability Pattern Classifier**: Provides a detailed classification, identifying the specific upgradeability proxy pattern that the detected UPC adheres to.

For each input contract address, UPC Sentinel produces a binary label indicating whether the contract is a UPC or not. If classified as a UPC, it further identifies the specific upgradeability proxy pattern associated with the contract.

![UPC Sentinel architecture](./UPC_Sentinel_Arch.JPG)

# UPC Sentinel V2

**UPC Sentinel** was originally designed to detect **active Upgradeability Proxy Contracts (UPCs)**. An *active UPC* refers to a proxy contract whose forwarding functionality (e.g., via `delegatecall`) has been used at least once after deployment. This detection relies on **dynamic analysis**, specifically, analyzing transactions that interact with the contract. Since dynamic analysis depends on actual transactional activity, **contracts with no interactions cannot be classified as proxies** using this method alone. However, within UPC Sentinel’s **Upgradeability Pattern Detector** layer, we’ve embedded a **static analysis component** that analyzes the **decompiled bytecode** of smart contracts. This static detection approach is functionally equivalent to dynamic analysis, with the added benefit of detecting **inactive proxies** (those with no on-chain activity). The trade-off is a potential reduction in scalability due to the need for bytecode decompilation.

We are currently in the process of **enabling this static component**, which will allow UPC Sentinel to detect **both active and inactive proxy contracts**.

> ⚠️ **Note**: For inactive proxies, even though we can identify that a contract is a proxy, we are currently **unable to extract its implementation address**. This is because doing so requires **reading on-chain storage** (specifically, the storage slot where the implementation address is saved), which involves interacting with the live blockchain, something static analysis alone cannot accomplish.

### ✅ The Good News

For several proxy pattern variants, it is possible to determine whether a contract is a UPC **without needing to read its storage**. As shown in the table below, **UPC Sentinel can detect both active and inactive proxies** for those patterns. For other patterns (particularly the last three), identifying the implementation address or external logic contract is essential for accurate classification, this is a capability we plan to introduce in a future update.

| Upgradeability Reference Design  | Upgradeability Proxy Pattern Variant                     | Active | Inactive |
|----------------------------------|----------------------------------------------------------|:------:|:--------:|
| SMUP                             | Inherited Storage Upgradeability Proxy                   | ✅     | ✅      |
| SMUP                             | Eternal Storage Upgradeability Proxy                     | ✅     | ✅      |
| SMUP                             | ERC-1967 Upgradeability Proxy (Unstructured Store)       | ✅     | ✅      |
| SMUP                             | Transparent Upgradeability Proxy                         | ✅     | ✅      |
| DUP                              | ERC-2535 Diamonds Upgradeability Proxy                   | ✅     | ✅      |
| DUP                              | ERC-1822 Universal Upgradeable Proxy                     | ✅     | ❌      |
| ESUP                             | Beacon Upgradeability Proxy                              | ✅     | ❌      |
| ESUP                             | Registry Upgradeability Proxy                            | ✅     | ❌      |


## 📁 Folder Structure

The repository is organized as follows:

- `benchmarks/`  
  Contains a set of upgradeable smart contract benchmarks collected from academic papers and gray literature. These contracts are verified using UPC Sentinel V2.

- `examples/`  
  Part of the replication package for the UPC Sentinel paper. This folder includes examples demonstrating cases where source code contains dead proxy contracts, leading to inaccuracies in source code-level UPC detectors.

- `findings/`  
  Part of the replication package for the UPC Sentinel paper. This folder includes the empirical results and findings related to all research questions (RQs) addressed in the UPC Sentinel paper.

- `groundtruths/`  
  Part of the replication package for the UPC Sentinel paper. This folder includes the two ground truth datasets used for evaluating UPC Sentinel’s detection performance. This is part of the replication package.

- `quality checks on ground truths/`  
  Part of the replication package for the UPC Sentinel paper. This folder documents the step-by-step process of identifying and correcting inaccuracies in one of the employed ground truth datasets to improve label quality and resolve misclassified instances.

- `src/`  
  Part of the replication package for the UPC Sentinel paper. This folder includes the source code for UPC Sentinel. This is the core detection tool evaluated and described in the accompanying paper.

# How to Setup Google BigQuery for Free

Google BigQuery is a powerful, scalable, and cost-effective multi-cloud data warehouse designed for business agility. This README provides step-by-step instructions to set up a free Google BigQuery account.

## Step 1: Create a Google Account

If you do not already have a Google account, you will need to create one:

1. Go to [Google Accounts](https://accounts.google.com/signup).
2. Follow the prompts to create your new Google account.

## Step 2: Sign Up for Google Cloud Platform

1. Visit the [Google Cloud Platform Console](https://console.cloud.google.com/).
2. Sign in with your Google account if you are not already logged in.
3. If this is your first time accessing Google Cloud Platform, you will need to agree to the terms of service and set up your Cloud account with your billing information.

## Step 3: Activate the Google Cloud Free Tier

Google Cloud offers a Free Tier which includes $300 in free credits to spend on Google Cloud services over the next 12 months and provides limited access to many common Google Cloud resources, including BigQuery.

1. Navigate to the [Google Cloud Free Tier page](https://cloud.google.com/free).
2. Click on the **Get started for free** button.
3. Enter your country, agree to the terms of service, and click **Continue**.
4. Complete the billing information (credit card and billing address). Your credit card will not be charged unless you upgrade to a paid account.
5. Once completed, you will have access to the $300 free credit.


# Setting Up Google BigQuery Client

This guide will walk you through setting up the Google Cloud BigQuery Client in your local development environment.

## Step 1: Set Up Your Environment

Ensure that Python (3.8.9) is installed on your machine. You will also need to install the Google Cloud BigQuery Client library and others. If it's not already installed, you can do so using `pip`. Open your terminal and run the following command:

```bash
pip install --upgrade google-cloud-bigquery
pip install overrides
pip install tqdm
pip install google-cloud-storage
```

## Step 2: Set Up Google Cloud Authentication

To interact with Google BigQuery, you need to authenticate your client application with Google Cloud. Follow these steps to set up authentication:

### Create a Google Cloud Project

- If you haven't already, create a project in the Google Cloud Console at [Google Cloud Console](https://console.cloud.google.com/).

### Enable the BigQuery API

- Ensure your project is selected in the Google Cloud Console.
- Navigate to the **APIs & Services** dashboard.
- Click on **+ ENABLE APIS AND SERVICES**.
- Search for **BigQuery API** and enable it for your project.

### Create a Service Account Key

1. **Navigate to Service Accounts**:
   - In the Google Cloud Console, go to **IAM & Admin > Service Accounts**.

2. **Create Service Account**:
   - Click **Create Service Account**.
   - Enter a name for the service account and click **Create**.

3. **Assign Role**:
   - Assign the **BigQuery Admin** and **Storage Admin** role (or a more restrictive role if necessary) from the role list and click **Continue**.

4. **Finish Creating Service Account**:
   - Click **Done** to complete the service account creation.

5. **Manage Service Account Keys**:
   - Click on the newly created service account for more options.
   - Go to the **Keys** tab.
   - Click **Add Key**, then select **Create New Key**.

6. **Download Key**:
   - Choose **JSON** as the key type and click **Create**. This will download the JSON key file to your machine.

# Running UPC Sentinel
1. **Install Panoramix**
2. **Place the Json key file in src/ directory**
3. **Configure Util.py with the Json key file name and other configurations**
```bash
DATA_DIR = os.path.abspath("../storage/") # path where files are downloaded
DECOMPILER_OUTPUT_DIR = os.path.join(DATA_DIR, 'decompiled-bytecodes') # path where panoramix writes its output decompiled bytecodes
DECOMPILER_TIMEOUT = 3600 # panormaix decompiler timeout
STUDY_START_DATE = "2015-01-01"
STUDY_END_DATE = "2022-09-01"
BQ_KEY_PATH = 'lateral-command-433401-d4-89aa899f9420.json' # Json key file name
BQ_PROJECT_ID = '-'.join(BQ_KEY_PATH.split("-")[:len(BQ_KEY_PATH.split("-")) -1])
BQ_STORAGE_PROXY_DETECTOR = 'storage_dynamic_proxy_detector'
BQ_STORAGE_BYTECODES = 'storage_bytecodes'
CORE_COUNT = int(multiprocessing.cpu_count() * 0.75) # 80 * .75 = 60 # number of cores for reading files and performing parallel decompilation.
```
4. **Prepare your list of input contract addresses**
   - This is a list of Ethereum Contract Accounts (CAs) stating with "0x" and in lower case format.
5. **Run Main.py with your list of input contract addresses**
   - Initialize Proxy Detector. To initialize the Proxy Detector for the first time, set the `init` parameter to `True`. This will trigger the identification and download of active proxy contracts. Once the initial download is complete, change the init parameter to False for subsequent runs. This prevents re-downloading the proxy contracts and instead reads the already stored objects from disk.
   - Initialize Bytecode Decompiler. To initialize the Bytecode Decompiler for the first time, set the `init` parameter to `True`. This will trigger the identification and download of bytecode objects. Once the initial download is complete, change the init parameter to False for subsequent runs. This prevents re-downloading bytecodes and instead reads the already stored objects from disk.
   - Read your input list of contract addresses (e.g., ['0xd54f502e184b6b739d7d27a6410a67dc462d69c8'])
   - Call the is_upc_batch(input_contract_addresses, beacon_dataset_name, early_stop = False) function
      - The early_stop=True will stop looking deeper into the contract as soon as it is detected as UPC.
      - Pick your beacon_dataset_name (i.e., the dataset of target depencdies that ESUP detector fetches). To avoid overriding the target depencies for each experiment (i.e., a set of input contracts), we recommend you pick a different name for each. For instances, 'df-beacons-uschunt' or 'df-beacons-etherscan'. Also, only use alphebtic characters along with hyphen as these are accepted naming convetions for Google BigQuery storage names.

## Citations

This project uses data and methodologies based on several foundational texts and papers. If you use this software, adapt its code, or incorporate its methodologies in academic or professional contexts, please consider citing the following two papers:

```
@misc{ebrahimi2024,
      title={UPC Sentinel: An Accurate Approach for Detecting Upgradeability Proxy Contracts in Ethereum}, 
      author={Amir M. Ebrahimi and Bram Adams and Gustavo A. Oliva and Ahmed E. Hassan},
      year={2024},
      eprint={2501.00674},
      archivePrefix={arXiv},
      primaryClass={cs.SE},
      url={https://arxiv.org/abs/2501.00674}, 
}

@article{Ebrahimi24,
  author = {Ebrahimi, Amir M. and Adams, Bram and Oliva, Gustavo A. and Hassan, Ahmed E.},
  title = {A large-scale exploratory study on the proxy pattern in Ethereum},
  journal = {Empirical Software Engineering},
  volume = {29},
  number = {4},
  pages = {81},
  year = {2024},
  month = {June},
  doi = {10.1007/s10664-024-10485-1},
  url = {https://doi.org/10.1007/s10664-024-10485-1},
  issn = {1573-7616}
}

```
