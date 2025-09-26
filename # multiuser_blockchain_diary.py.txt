# multiuser_blockchain_diary.py

import streamlit as st
import hashlib
import datetime

# ---------------- Blockchain Logic ----------------

class Block:
    def __init__(self, index, timestamp, user, data, previous_hash):
        self.index = index
        self.timestamp = timestamp
        self.user = user
        self.data = data
        self.previous_hash = previous_hash
        self.hash = self.calculate_hash()
    
    def calculate_hash(self):
        block_string = f"{self.index}{self.timestamp}{self.user}{self.data}{self.previous_hash}"
        return hashlib.sha256(block_string.encode()).hexdigest()

class Blockchain:
    def __init__(self):
        self.chain = [self.create_genesis_block()]
    
    def create_genesis_block(self):
        return Block(0, str(datetime.datetime.now()), "System", "Genesis Block", "0")
    
    def get_last_block(self):
        return self.chain[-1]
    
    def add_block(self, user, data):
        last_block = self.get_last_block()
        new_block = Block(
            index=last_block.index + 1,
