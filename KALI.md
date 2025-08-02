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

## Regular Expression
Great — now using `/etc/ssh/sshd_config` as the target file, here are the specific Linux commands for your tasks:

---

### 1. **Show all lines that do not contain the `#` character:**

```bash
grep -v '#' /etc/ssh/sshd_config
```

> Shows only uncommented or partially uncommented lines.

---

### 2. **Search for all lines that contain a word that starts with `Permit`:**

```bash
grep -E '\bPermit\w*' /etc/ssh/sshd_config
```

> Matches lines with words like `PermitRootLogin`, `PermitEmptyPasswords`, etc.

---

### 3. **Search for all lines that contain a word ending with `Authentication`:**

```bash
grep -E '\w*Authentication\b' /etc/ssh/sshd_config
```

> Matches lines like `PasswordAuthentication`, `ChallengeResponseAuthentication`, etc.

---

### 4. **Search for all lines containing the word `Key`:**

```bash
grep 'Key' /etc/ssh/sshd_config
```

> Matches any line with `Key`, e.g. `HostKey`, `AuthorizedKeysFile`.

---

### 5. **Search for all lines beginning with `Password` and containing `yes`:**

```bash
grep -E '^Password.*yes' /etc/ssh/sshd_config
```

> For example, matches: `PasswordAuthentication yes`.

---

### 6. **Search for all lines that end with `yes`:**

```bash
grep 'yes$' /etc/ssh/sshd_config
```

> Matches lines where `yes` is at the end — common in config options like `X11Forwarding yes`.

---

### Resource
https://academy.hackthebox.com/module/18/section/2092
