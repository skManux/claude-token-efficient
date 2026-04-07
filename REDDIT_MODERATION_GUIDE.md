# Reddit AutoModerator Setup Guide

## How to Deploy

1. Go to your subreddit settings
2. Click **Moderation tools** > **Automoderator**
3. Copy entire `AUTOMODERATOR_CONFIG.yaml` content
4. Paste into AutoModerator config editor
5. Click **Save**

---

## What This Config Does

### REMOVES (Auto-delete):
- Low-effort negative comments ("this sucks", "trash", no substance)
- Spam and self-promotion links
- Toxic/trolling patterns
- Short dismissive comments (< 20 chars without reason)
- Misinformation about pricing (claims without evidence)

### APPROVES (Bypasses filter):
- Constructive criticism with specific details
- Bug reports with reproduction steps
- Questions asking how/why
- Links to evidence (GitHub, code examples)
- Praise/thanks messages

### FLAGS FOR REVIEW (Modmail notification):
- Potential bug reports (uses word "broken" but detailed)
- Controversial but substantive comments

### AUTO-REPLIES:
- When someone says "doesn't work" without details
- Asks for: expected behavior, actual behavior, steps
- Points to GitHub issues

---

## Customize for Your Community

**Change aggressive comments threshold:**
```yaml
body_length: "< 20"  # Change to < 30 or < 50
```

**Add more approved keywords:**
```yaml
body (regex):
  - "my benchmark|my test|empirical data"
```

**Whitelist specific users:**
```yaml
author:
  name: ["mod1", "mod2"]
action: approve
```

**Auto-remove multiple reports:**
```yaml
reports: ">= 3"
action: remove
```

---

## Monitor Results

- Check **Modqueue** daily (removed comments await review)
- Review flagged comments in **Modmail**
- Adjust regex patterns if too strict/lenient
- Keep logs of common patterns removed

---

## Quick Regex Reference

| Pattern | Matches |
|---------|---------|
| `(?i)word` | Case-insensitive "word" |
| `^text` | Comment starts with "text" |
| `text$` | Comment ends with "text" |
| `word1\|word2` | Either "word1" or "word2" |
| `.{20,}` | 20+ characters |
| `http(?:s)?://` | Any URL |

---

## Test Before Live Deploy

1. Set to `filter` instead of `remove` first
2. Monitor modqueue for 24 hours
3. Check if wanted comments get filtered
4. Adjust patterns
5. Switch to `remove` once tuned

