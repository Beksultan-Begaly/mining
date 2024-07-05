import hashlib
import time

def mine(block_number, transactions, previous_hash, prefix_zeros):
    nonce = 0
    prefix_str = '0' * prefix_zeros

    while True:
        text = str(block_number) + transactions + previous_hash + str(nonce)
        new_hash = hashlib.sha256(text.encode('utf-8')).hexdigest()
        if new_hash.startswith(prefix_str):
            print(f"Successfully mined with nonce value:{nonce}")
            return new_hash
        nonce += 1

if __name__ == '__main__':
    block_number = 1
    transactions = "Alice pays Bob 10 BTC"
    previous_hash = "00000000000000000000000000000000"
    prefix_zeros = 4

    start_time = time.time()
    new_hash = mine(block_number, transactions, previous_hash, prefix_zeros)
    total_time = str((time.time() - start_time))
    print(f"Mining took: {total_time} seconds")
    print(f"New hash: {new_hash}")
