# pip install requests
import requests
import time

# TODO: set your config
api_key = "YOUR_API_KEY"  # your api key of capsolver
site_key = "00000000-0000-0000-0000-000000000000"  # site key of your target site
site_url = "https://www.yourwebsite.com"  # page url of your target site


def capsolver():
    payload = {
        "clientKey": api_key,
        "task": {
            "type": 'HCaptchaTaskProxyLess',
            "websiteKey": site_key,
            "websiteURL": site_url
        }
    }
    res = requests.post("https://api.capsolver.com/createTask", json=payload)
    resp = res.json()
    task_id = resp.get("taskId")
    if not task_id:
        print("Failed to create task:", res.text)
        return
    print(f"Got taskId: {task_id} / Getting result...")

    while True:
        time.sleep(1)  # delay
        payload = {"clientKey": api_key, "taskId": task_id}
        res = requests.post("https://api.capsolver.com/getTaskResult", json=payload)
        resp = res.json()
        status = resp.get("status")
        if status == "ready":
            return resp.get("solution", {}).get('gRecaptchaResponse')
        if status == "failed" or resp.get("errorId"):
            print("Solve failed! response:", res.text)
            return


token = capsolver()
print(token)
