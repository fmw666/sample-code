# sorted

## 多条件排序

第一条件为：num 升序

第二条件为：指定结果优先，如同样 num == 2，规定如果 name == "fmw"，则排在最后

```py
lst = [
    {"num": 2, "name": "fmw"},
    {"num": 3, "name": "ttt"},
    {"num": 1, "name": "qqq"},
    {"num": 4, "name": "zzz"},
    {"num": 2, "name": "ppp"},
    {"num": 4, "name": "www"},
    {"num": 2, "name": "ccc"},
]

s = sorted(lst, key=lambda x: (x["num"], x["name"]=="fmw"))
```

如果想让 第二条件中，name == "fmw" 排在最前：

```py
lst = [
    {"num": 2, "name": "fmw"},
    {"num": 3, "name": "ttt"},
    {"num": 1, "name": "qqq"},
    {"num": 4, "name": "zzz"},
    {"num": 2, "name": "ppp"},
    {"num": 4, "name": "www"},
    {"num": 2, "name": "ccc"},
]

s = sorted(lst, key=lambda x: (x["num"], x["name"]!="fmw"))
# 如果第一条件是数字可以采用这种方式
s = sorted(lst, key=lambda x: (-x["num"], x["name"]=="fmw"), reverse=True)
```
