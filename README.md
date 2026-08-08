# 🪐 YonHub

**A registry of libraries for YonderScript.**

Install any library from here, from anywhere:

```bash
export YON_REGISTRY=https://raw.githubusercontent.com/jybadawi/yonhub/main
yon install jokes
```

Then use it:

```
bring "jokes"
say jokes.tell()
```

Or grab one directly by URL:

```bash
yon install https://raw.githubusercontent.com/jybadawi/yonhub/main/convert.ys
```

## 📦 Available libraries

| Library | What it does | Example |
| --- | --- | --- |
| **jokes** | random programming jokes | `say jokes.tell()` |
| **convert** | unit conversions (temp, distance, weight) | `say convert.c_to_f(100)` |

## ➕ Add your own

Drop a `.ys` file in this repo, add its name to `index`, and push. It's instantly installable with `yon install <name>`.
