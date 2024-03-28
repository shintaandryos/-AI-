# -AI-
スマート物流は、ブロックチェーン技術と機械学習を活用して、サプライチェーン全体の可視化と最適化を実現し、物流のコスト削減と効率化を図ります。
# Part 1: Basic Blockchain Implementation
import hashlib
import time
from sklearn.linear_model import LinearRegression
import numpy as np

class Block:
    def __init__(self, index, transactions, timestamp, previous_hash):
        self.index = index
        self.transactions = transactions
        self.timestamp = timestamp
        self.previous_hash = previous_hash
        self.hash = self.calculate_hash()

    def calculate_hash(self):
        block_string = f"{self.index}{self.transactions}{self.timestamp}{self.previous_hash}"
        return hashlib.sha256(block_string.encode()).hexdigest()

class Blockchain:
    def __init__(self):
        self.chain = []
        self.create_genesis_block()

    def create_genesis_block(self):
        genesis_block = Block(0, [], time.time(), "0")
        self.chain.append(genesis_block)

    def add_block(self, transactions):
        last_block = self.chain[-1]
        new_block = Block(len(self.chain), transactions, time.time(), last_block.hash)
        self.chain.append(new_block)

    def is_valid(self):
        for i in range(1, len(self.chain)):
            current = self.chain[i]
            previous = self.chain[i - 1]
            if current.hash != current.calculate_hash():
                return False
            if current.previous_hash != previous.hash:
                return False
        return True

# Part 2: Simple AI for Predictive Analytics
# Dummy data: [week, demand]
data = np.array([
    [1, 100],
    [2, 150],
    [3, 200],
    [4, 250],
    [5, 300],
])

X = data[:, 0].reshape(-1, 1)  # weeks
y = data[:, 1]  # demand

# Train a simple linear regression model
model = LinearRegression().fit(X, y)

# Predict future demand
