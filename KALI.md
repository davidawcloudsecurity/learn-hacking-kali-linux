## Filter Contents
---

### 1. **A line with the username `cry0l1t3`:**

```bash
grep '^cry0l1t3:' /etc/passwd
```

---

### 2. **The usernames:**

```bash
cut -d: -f1 /etc/passwd
```

---

### 3. **The username `cry0l1t3` and his UID:**

```bash
grep '^cry0l1t3:' /etc/passwd | cut -d: -f1,3
```

---

### 4. **The username `cry0l1t3` and his UID separated by a comma (,):**

```bash
grep '^cry0l1t3:' /etc/passwd | awk -F: '{print $1","$3}'
```

---

### 5. **The username `cry0l1t3`, his UID, and the set shell separated by a comma (,):**

```bash
grep '^cry0l1t3:' /etc/passwd | awk -F: '{print $1","$3","$7}'
```

---

### 6. **All usernames with their UID and set shells separated by a comma (,):**

```bash
awk -F: '{print $1","$3","$7}' /etc/passwd
```

---

### 7. **All usernames with their UID and set shells separated by a comma (,) and exclude the ones that contain `nologin` or `false`:**

```bash
awk -F: '!/nologin|false/ {print $1","$3","$7}' /etc/passwd
```

---

### 8. **All usernames with their UID and set shells separated by a comma (,) and exclude the ones that contain `nologin`, then count all lines of the filtered output:**

```bash
awk -F: '!/nologin/ {print $1","$3","$7}' /etc/passwd | wc -l
```

---

### Resource
https://academy.hackthebox.com/module/18/section/80
