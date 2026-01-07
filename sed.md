
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


