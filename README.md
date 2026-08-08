# 🪐 YonHub

**A registry of libraries for YonderScript.**

### 👉 New to YonderScript? **[Read the full tutorial: LEARN.md](LEARN.md)**

Install any library with one command:

```bash
yon install jokes
```

Then use it:

```
bring "jokes"
say jokes.tell()
```

(Installs come from this repo by default. Or grab one by URL:
`yon install https://raw.githubusercontent.com/jybadawi/yonhub/main/convert.ys`)

## 📦 Available libraries

| Library | What it does | Example |
| --- | --- | --- |
| **strings** | text helpers: title, reverse, repeat, pad | `strings.title("hi there")` |
| **lists** | map / filter / reduce, sort, first, last | `lists.map([1,2,3], fn(x) => x*2)` |
| **mathx** | factorial, gcd, lcm, isprime, clamp, sqrt | `mathx.isprime(97)` |
| **dates** | today, now, year, weekday | `dates.today()` |
| **chance** | dice, coin, shuffle, random picks | `chance.dice()` |
| **color** | color terminal text (ANSI) | `color.green("ok!")` |
| **money** | format money & big numbers | `money.dollars(1234.5)` |
| **validate** | check emails, numbers, phones | `validate.is_email("a@b.com")` |
| **convert** | unit conversions (temp, distance, weight) | `convert.c_to_f(100)` |
| **jokes** | random programming jokes | `jokes.tell()` |

## ➕ Add your own

Drop a `.ys` file in this repo, add its name to `index`, and push — it's instantly installable with `yon install <name>`.
