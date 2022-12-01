# 服务注册

## 快速启用

```py
import requests

headers = {
    "contentType": "application/json"
}

def register(name, id, tags, address, port):
    url = "http://127.0.0.1:8500/v1/agent/service/register"
    rsp = requests.put(url, headers=headers, json={
        "Name": name,
        "ID": id,
        "Tags": tags,
        "Address": address,
        "Port": ports
    })
    if rsp.status_code == 200:
        print("注册成功")
    else:
        print(f"注册失败：{rsp.status_code}")

if __name__ == "__main__":
    register("user_srv", "user_srv", [], "127.0.0.1", 50051)
```

## 健康检查

### http

```py
import requests

headers = {
    "contentType": "application/json"
}

def register(name, id, tags, address, port):
    url = "http://127.0.0.1:8500/v1/agent/service/register"
    rsp = requests.put(url, headers=headers, json={
        "Name": name,
        "ID": id,
        "Tags": tags,
        "Address": address,
        "Port": ports,
        "Check": {
            "HTTP": f"http://{address}:{port}/health",
            "Timeout": "5s",
            "Interval": "5s",
            "DeregisterCriticalServiceAfter": "15s"
        }
    })
    if rsp.status_code == 200:
        print("注册成功")
    else:
        print(f"注册失败：{rsp.status_code}")

if __name__ == "__main__":
    register("user_srv", "user_srv", [], "127.0.0.1", 50051)
```

### grpc

```py
import requests

headers = {
    "contentType": "application/json"
}

def register(name, id, tags, address, port):
    url = "http://127.0.0.1:8500/v1/agent/service/register"
    rsp = requests.put(url, headers=headers, json={
        "Name": name,
        "ID": id,
        "Tags": tags,
        "Address": address,
        "Port": ports,
        "Check": {
            "GRPC": f"{address}:{port}",
            "GRPCUseTLS": False,
            "Timeout": "5s",
            "Interval": "5s",
            "DeregisterCriticalServiceAfter": "15s"
        }
    })
    if rsp.status_code == 200:
        print("注册成功")
    else:
        print(f"注册失败：{rsp.status_code}")

if __name__ == "__main__":
    register("user_srv", "user_srv", [], "127.0.0.1", 50051)
```
