
08-January-2026


---

# 📝 Notes on `sed` Command (Find & Replace)

## 🔹 Basic Syntax
```bash
sed 's/find/replace/' file.txt
```
- **`s`** → substitute (replace text).  
- **`find`** → the word/pattern you want to search.  
- **`replace`** → the word/pattern you want to replace it with.  
- **`file.txt`** → the file where the replacement happens.  

👉 By default, only the **first occurrence per line** is replaced.

---

## 🔹 Example
Create a file:
```bash
cat > geekfile.txt
unix is great os. unix is opensource. unix is free os.
```

Run `sed`:
```bash
sed 's/unix/linux/' geekfile.txt
```

### Output:
```
linux is great os. unix is opensource. unix is free os.
```

- Notice: Only the **first "unix" in each line** was replaced with **linux**.

---

## 🔹 Key Tip
- To replace **all occurrences** in each line, add the `g` flag:
```bash
sed 's/unix/linux/g' geekfile.txt
```

---

### Question: sh "sed -i 's+raj80dockerid/test.*+raj80dockerid/test:${DOCKERTAG}+g' deployment.yaml"
what is + sign here

In the `sed` command, the `+` sign is acting as a **delimiter** (a separator).

Usually, people use the forward slash `/` as the separator, like this: `sed 's/find/replace/'`. However, `sed` is very flexible—it allows you to use almost any character (like `+`, `#`, `|`, or `:`) as a separator instead of `/`.

### **Why use `+` instead of `/`?**

In your specific case, you are dealing with a **Docker Image name**: `raj80dockerid/test`.

Notice that the image name already contains a forward slash (`/`). If you used the standard `/` delimiter, the command would look like this mess:
`sh "sed -i 's/raj80dockerid/test.*/raj80dockerid/test:${DOCKERTAG}/g'"`

**The Problem:** The computer sees **5 different slashes** and gets confused. It can't tell which slash is part of the image name and which one is supposed to separate the "find" and "replace" sections. This results in a "Trailing characters" or "Pattern not found" error.

### **The Solution: Pick a Different Delimiter**

By using `+`, the command becomes clean and easy for the computer to read:
`s + [FIND THIS] + [REPLACE WITH THIS] + g`

---

### **Breakdown of the "Find" and "Replace" sections:**

1. **Find:** `raj80dockerid/test.*`
2. **Replace:** `raj80dockerid/test:${DOCKERTAG}`
3. **The "Glue":** The `+` signs separate these two sections so the slash inside `raj80dockerid/test` doesn't cause an error.

---

### **Other Examples**

You can use any symbol that **is not** inside your text. All of these do the exact same thing:

* Using `#`: `sed 's#find#replace#g'`
* Using `|`: `sed 's|find|replace|g'`
* Using `+`: `sed 's+find+replace+g'` (This is what you have!)

**Summary for your notes:**

> "The `+` is a **custom delimiter**. We use it because our Docker image name contains a `/`, which would confuse `sed` if we used the standard `/` separator."

---


### Question2 "The `*` (combined as `.*`)
