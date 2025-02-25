
# Federated Learning with Flower and PyTorch on MNIST Dataset

This project demonstrates a federated learning setup using the Flower framework and PyTorch. 
The MNIST dataset is partitioned across multiple clients, each training a model on their own data 
and sending updates back to the server for aggregation. Clients 9 and 10 have poisoned data 
(with label flipping) to simulate adversarial clients.

## Setup and Requirements

1. **Dependencies**:
   - Python 3.7+
   - Install the required libraries:
     ```bash
     pip install flwr torch torchvision matplotlib pandas
     ```

2. **Folder Structure**:
   - Place this script and all code files in a single directory.
   - Ensure a subdirectory called `data/mnist/` exists within this directory to store the MNIST dataset.

## Data Preparation

1. **Download and Partition the MNIST Dataset**:
   - Run `prepare_data.py` to download the MNIST dataset and split it into partitions for each client:
     ```bash
     python prepare_data.py
     ```
   - This will create 10 partitions in the `data/mnist/` directory. Clients 9 and 10 will contain poisoned data, 
     where labels have been randomly flipped.

## Code Overview

1. **Server Code** (`server.py`):
   - This script initializes and starts the Flower server, which coordinates federated learning among the clients.
   - The server implements a custom aggregation strategy with Trust and Reputation mechanisms to mitigate the influence of poisoned clients.
   - At the end of training, the server will generate plots showing the training progress, loss, and accuracy.

2. **Client Code** (`client.py`):
   - Each client runs a PyTorch-based model on its local data and communicates with the server.
   - Clients 9 and 10 have poisoned data due to label flipping, which allows us to observe the effect of the Trust and Reputation mechanisms on model performance.

## Running the Code

1. **Start the Server**:
   - Open a terminal and run the server:
     ```bash
     python server.py
     ```

2. **Start the Clients**:
   - In separate terminals, start each client by setting a unique client ID:
     ```bash
     CLIENT_ID=0 python client.py
     CLIENT_ID=1 python client.py
     ...
     CLIENT_ID=9 python client.py
     ```
   - You need 10 terminals or terminal tabs to start each client with IDs from 0 to 9. 

## Results and Plots

After all federated rounds complete, the server will generate the following plots:
1. **History of loss per client over rounds**
2. **History of average loss among clients over rounds**
3. **History of evaluation accuracy per client over rounds**
4. **History of average evaluation accuracy among clients over rounds**
