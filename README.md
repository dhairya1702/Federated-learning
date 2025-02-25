
# 🚀 Federated Learning with Flower & PyTorch on MNIST  

This project demonstrates a **federated learning** setup using **Flower** 🌸 and **PyTorch** 🔥.  
The **MNIST dataset** 🖼️ is partitioned across multiple clients, each training a model on their local data before sending updates to the central **server** 🖥️ for aggregation.  

To simulate **adversarial clients**, **Clients 9 & 10** contain **poisoned data** 🧪 (label flipping).  

The server implements a **Trust and Reputation Mechanism** 🏆 to mitigate their influence.

---

## ⚙️ Setup & Requirements 

1. **Dependencies**:
   - Python 3.7+
   - Install the required libraries:
     ```bash
     pip install flwr torch torchvision matplotlib pandas
     ```

2. **Folder Structure**:
   - Place this script and all code files in a single directory.
   - Ensure a subdirectory called `data/mnist/` exists within this directory to store the MNIST dataset.
   - 

## 📊 Data Preparation

1. **📉 Download and Partition the MNIST Dataset**:
   - Run `prepare_data.py` to download the MNIST dataset and split it into partitions for each client:
     ```bash
     python prepare_data.py
     ```
This will:

     ✅ Download the MNIST dataset 🖼️
     ✅ Create 10 partitions inside data/mnist/ 📂
     ✅ Poison Clients 9 & 10 with random label flipping 🧪


## 🔍 Code Overview  

### 🖥️ **Server Code** (`server.py`)  
- Initializes and starts the **Flower Federated Learning Server** 🌸.  
- Implements a **custom aggregation strategy** with **Trust & Reputation mechanisms** 🏆.  
- Generates **accuracy & loss plots** 📊.  

### 🤖 **Client Code** (`client.py`)  
- Each client trains a **PyTorch-based model** locally and communicates with the server.  
- **Clients 9 & 10** contain **poisoned data** for adversarial testing 🧪.  

## 🚀 Running the Code  

1. **🏁 Start the Server**:
   - Open a terminal and run the server:
     ```bash
     python server.py
     ```

2. **🤖 Start the Clients**:
   - In separate terminals, start each client by setting a unique client ID:
     ```bash
     CLIENT_ID=0 python client.py
     CLIENT_ID=1 python client.py
     ...
     CLIENT_ID=9 python client.py
     ```
   - You need 10 terminals or terminal tabs to start each client with IDs from 0 to 9. 

## 📈 Results & Plots  

After all **federated rounds** complete, the **server** will generate the following visualizations:  

🔹 **Loss Trends**  
   - 📉 **Loss per client** over rounds  
   - 📊 **Average loss** across all clients  

🔹 **Accuracy Trends**  
   - ✅ **Evaluation accuracy per client** over rounds  
   - 📈 **Average evaluation accuracy** among all clients  

These plots help **analyze model performance** and the **impact of poisoned clients** on federated learning.  

