import requests
import random
import string
import time
import os
from colorama import Fore, Back, Style, init
init(autoreset=True)

logo = f"""


  {Fore.YELLOW}█   █ █▀▀ █▀▀ █▀▄   {Fore.MAGENTA}█▀▀ █ █ █▀▀ █▀▀ █ █ █▀▀ █▀▄ 
  {Fore.YELLOW}█   █ ▀▀█ █▀▀ █▀▄   {Fore.MAGENTA}█   █▀█ █▀▀ █   █▀▄ █▀▀ █▀▄
  {Fore.YELLOW}▀▀▀▀▀ ▀▀▀ ▀▀▀ ▀ ▀   {Fore.MAGENTA}▀▀▀ ▀ ▀ ▀▀▀ ▀▀▀ ▀ ▀ ▀▀▀ ▀▀  
           
              {Fore.RED}By: LIder{Fore.CYAN}                    

"""

def send_to_telegram(message, token, chat_id):
    if token and chat_id:
        try:
            url = f"https://api.telegram.org/bot{token}/sendMessage"
            data = {
                "chat_id": chat_id,
                "text": message
            }
            response = requests.post(url, data=data)
            return response.json()
        except Exception as e:
            print(f"{Fore.RED}Error sending message to Telegram: {e}")
    else:
        print(f"{Fore.RED}Telegram not configured. Please enter valid token and chat ID.")
        
def check_username(username, token, chat_id):
    url = "https://app.snapchat.com/loq/suggest_username_v3"
    headers = {
        "User-Agent": "Snapchat/12.43.0.32 (Agile_Client_Error; Android 11; gzip)"
    }
    data = {
        "requested_username": username,
        "x-niggers": "RE8gTk9UIERFQ09ERSA6IFpHbHpZMjl5WkM1blp5OXZibXh3SURzZ0tRPT0=",
    }

    try:
        r = requests.post(url, headers=headers, data=data).text

        if "DELETED" in r:
            return "banned"
        elif "TAKEN" in r:
            return "taken"
        elif "OK" in r and "DELETED" not in r and "TAKEN" not in r:
            message = f"✅ Username : {username}\nBy: @LIdeeeeeer"
            send_to_telegram(message, token, chat_id)
            return "available"
        elif "TOO_SHORT" in r:
            return "too short"
        elif "Oops! Usernames must start with a letter" in r:
            return "must start with a letter"
        else:
            return f"Unknown error: {r}"
    except Exception as e:
        return f"Connection error: {e}"

def generate_username(length):
    letters = string.ascii_lowercase
    return ''.join(random.choice(letters) for i in range(length))

def main():
    print(logo)
    

    token = input(f"{Fore.WHITE}Enter Token: ")
    chat_id = input(f"{Fore.WHITE}Enter ID: ")
    
    while True:
        print(f"\n{Fore.BLUE}════════════════════════════════")
        print(f"{Fore.CYAN}1 - {Fore.WHITE}3char")
        print(f"{Fore.CYAN}2 - {Fore.WHITE}4char")
        print(f"{Fore.CYAN}3 - {Fore.WHITE}5char")
        print(f"{Fore.CYAN}4 - {Fore.WHITE}Specific")
        print(f"{Fore.CYAN}5 - {Fore.RED}Exit")

        choice = input(f"\n{Fore.GREEN}Your choice: ")

        if choice == '1':
            check_random_usernames(3, token, chat_id)
        elif choice == '2':
            check_random_usernames(4, token, chat_id)
        elif choice == '3':
            check_random_usernames(5, token, chat_id)
        elif choice == '4':
            username = input(f"{Fore.YELLOW}Enter username: ")
            result = check_username(username, token, chat_id)
            if result == "available":
                print(f"{Fore.GREEN}✅ Username : {username}")
            elif result == "banned":
                print(f"{Fore.RED}❌ Username banned: {username}")
            elif result == "taken":
                print(f"{Fore.RED}❌ Username taken: {username}")
            else:
                print(f"{Fore.YELLOW}⚠️ {result}")
        elif choice == '5':
            print(f"{Fore.MAGENTA}Thank you for using the tool!")
            break
        else:
            print(f"{Fore.RED}Invalid choice, please try again.")

def check_random_usernames(length, token, chat_id):

    delay = 7
    
    available = 0
    banned = 0
    taken = 0

    
    try:
        while True:
           
            username = generate_username(length)

            result = check_username(username, token, chat_id)

            if result == "available":
                available += 1
                print(f"{Fore.GREEN}✅ Username : {username}")
            elif result == "banned":
                banned += 1
                print(f"{Fore.RED}❌ Username banned: {username}")
            elif result == "taken":
                taken += 1
                print(f"{Fore.RED}❌ Username taken: {username}")
            else:
                print(f"{Fore.YELLOW}⚠️ {result}")

           
            time.sleep(delay)
            
    except KeyboardInterrupt:
        print(f"\n{Fore.MAGENTA}Check interrupted by user!")
        print(f"{Fore.CYAN}════════════════ Summary ════════════════")
        print(f"{Fore.WHITE}Total usernames checked: {count}")
        print(f"{Fore.GREEN}Available usernames: {available}")
        print(f"{Fore.RED}Banned usernames: {banned}")
        print(f"{Fore.RED}Taken usernames: {taken}")

if __name__ == "__main__":
    main()
