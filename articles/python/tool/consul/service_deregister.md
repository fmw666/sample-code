# 服务注销

```py
import requests

headers = {
    "contentType": "application/json"
}

def deregister(id):
    url = f"http://127.0.0.1:8500/v1/agent/service/deregister/{id}"
    rsp = requests.put(url, headers=headers)
    if rsp.status_code == 200:
        print("注销成功")
    else:
        print(f"注销失败：{rsp.status_code}")

if __name__ == "__main__":
    deregister("user_srv")
```