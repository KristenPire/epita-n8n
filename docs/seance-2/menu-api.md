# The API Menu 🍽

> Sources that are **tested and known to work** in this room. For Ex 2.1, **source 1 must
> come from this menu**. Source 2 can come from anywhere else (30 minutes of searching
> maximum, then you come back to the menu — that is the rule).

!!! note "Why a menu and not 'find your own API'?"
    You are 20+ people behind one IP address. Half the free APIs on the internet will rate
    limit you at the same second. The menu is the set that survives that.

## 🟢 No key, no account — zero friction

### Hacker News (search) — `already used in Séance 1`
```
https://hn.algolia.com/api/v1/search?query=YOUR_WORD&tags=story
https://hn.algolia.com/api/v1/search_by_date?query=YOUR_WORD&tags=story
```
- **Returns**: `hits[]` with `title`, `url`, `points`, `created_at`
- **Good for**: tech, SaaS, products, startup and market trends
- **Trap**: English only.

### RSS feeds — the press of any sector
n8n's **RSS Read** node reads any feed. Almost every outlet has one. Search
`"<outlet name>" RSS feed`.

Examples to adapt *(check them, outlets move their feeds)*:

| Sector | Feed |
|---|---|
| International tech | `https://techcrunch.com/feed/` |
| Tech FR | `https://www.usine-digitale.fr/rss` |
| Research / AI preprints | arXiv feeds, one per category |
| Retail / food / logistics | FashionNetwork, LSA, sector outlets |

- **Returns**: one item per article: `title`, `link`, `pubDate`, `content`
- **Good for**: watching any sector. The universal fallback source
- **Trap**: some feeds put the text in `content`, others in `contentSnippet`. Check OUTPUT
  (reflex 2).

### arXiv (research papers, no key)
```
http://export.arxiv.org/api/query?search_query=all:YOUR_TOPIC&start=0&max_results=20&sortBy=submittedDate&sortOrder=descending
```
- **Returns**: Atom XML, not JSON. n8n has an **XML** node to convert it
- **Good for**: anything research-related. Very relevant for Séance 3 Family C
- **Trap**: the response is XML. Convert first, then read fields.

### data.gouv.fr / open data
```
https://www.data.gouv.fr/api/1/datasets/?q=YOUR_TOPIC
```
- **Good for**: regulated markets, housing, health, mobility, agriculture. Official French
  data
- **Trap**: deeply nested response. Expect 2 more layers of objects than usual.

### Open-Meteo (weather, no key)
```
https://api.open-meteo.com/v1/forecast?latitude=48.85&longitude=2.35&daily=temperature_2m_max&timezone=Europe/Paris
```
- **Good for**: logistics, events, food service. Use it only if weather really matters to
  the use case.

### GitHub REST API (no key for public, read-only)
```
https://api.github.com/search/repositories?q=YOUR_TOPIC&sort=stars&order=desc
https://api.github.com/repos/OWNER/REPO/pulls?state=open
```
- **Returns**: `items[]` or a list of pull requests
- **Good for**: everything in Séance 3 Family B
- **Trap**: 60 requests per hour without a token, and that limit is shared by the whole
  room's IP. Add a personal token (free, 1 minute) and it becomes 5000 per hour.

## 🟡 Personal key — 2 minutes, free, yours

### NewsAPI (general press, several languages)

!!! note "Why a personal key and not one shared key?"
    An API key is a counter, not a password. Almost every free API caps you at X calls per
    period. NewsAPI gives 100 calls per day, per account. A key shared by 20 people does not
    change the cap, it divides it by 20. It dies in minutes, and the next person gets
    `429 Too Many Requests`. A personal key = your own quota.

    It is also a real reflex: getting your own API key in 2 minutes is a skill you need in
    Séance 3.

**CP0 — Get your key**

1. Go to `https://newsapi.org/register`.
2. Fill the form (email, password) → **Submit**. No credit card.
3. The key appears on the next page and also arrives by email.
4. Copy it somewhere safe. **Never** paste it in a public Slack message.

??? tip "Hint 1"
    Nothing received? Check spam, or regenerate it from `https://newsapi.org/account`.

??? tip "Hint 2"
    In n8n, paste the key into the **HTTP Request** node as the `apiKey` query parameter. No
    need for a dedicated credential in this exercise.

```
https://newsapi.org/v2/everything?q=YOUR_WORD&language=en&apiKey=YOUR_PERSONAL_KEY
```
- **Returns**: `articles[]` with `title`, `description`, `url`, `source.name`, `publishedAt`
- **Good for**: news in your language, consumer brands, named competitors
- **Traps**: the key is in the URL, so never share the full URL · non-commercial use only ·
  100 calls per day.

## 🔵 Your own data

### Google Sheets
Your FoodFleet sandbox, or any sheet shared with the `Workshop Google` account.
**Good for**: playing the role of a CRM or an internal database inside a pipeline.

### Incoming webhook
Your Ex 1.2 **is** a data source. **Good for**: forms, buttons, any external event.

---

## How to choose your 2 sources for Ex 2.1

1. **Source 1 (guaranteed)**: take the one closest to the FoodFleet case from this menu.
   When in doubt → a sector RSS feed.
2. **Source 2 (best effort)**: you may hunt for another API. ⏱ 30 minutes maximum, real
   clock. Cannot find one, or it misbehaves? Come back to the menu and take a second entry.
   No shame. The data matters more than the trophy.
3. The two must be **different types**. Not the same feed twice with two keywords.
