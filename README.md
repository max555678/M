from colorama import init, Fore, Style
import time
import secrets
from random import randint

# Initialize colorama
init()

BTC_VALUE = 31025  # Current value of Bitcoin in USD
MAX_ITERATIONS = 1000  # Maximum number of iterations for the simulation
CHANCE = 2500  # Chance factor for generating a rewarded transaction

def generate_transaction(btc_value):
    """Simulate a random transaction with a potential BTC reward."""
    ran_int = randint(0, CHANCE)
    if ran_int <= 1:
        random_btc = randint(1, 1000) / 100
        hex_token = secrets.token_hex(randint(17, 22))
        usd_value = f"{btc_value * random_btc:,.2f}"
        print(f"{Fore.WHITE}> 0x{hex_token} {Fore.GREEN}> {random_btc} BTC (${usd_value})")
        return True
    else:
        print(f"{Fore.WHITE}> {secrets.token_hex(randint(17, 22))} {Fore.RED}> 0.00 BTC ($0.00)")
        return False

def main():
    print(Fore.BLUE + "> Please put in your Bitcoin Wallet Address: ", end="")
    wallet = input()
    if not wallet:
        print(Fore.RED + "Invalid wallet address. Exiting...")
        return

    continuing = True
    for _ in range(MAX_ITERATIONS):
        if not continuing:
            break
        time.sleep(0.01)
        if generate_transaction(BTC_VALUE):
            answer = input(Fore.YELLOW + "> Would you like to continue? (Y/N): ").strip().lower()
            continuing = answer == "y"

    print(Fore.CYAN + "Simulation ended. Thank you for participating!")

if __name__ == "__main__":
    main()
