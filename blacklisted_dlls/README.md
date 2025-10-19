# Blacklisted DLLs Folder

## 📁 Purpose

This folder contains DLLs that should be blacklisted by the anticheat.

Place any DLL you want to blacklist here, and the anticheat will automatically:
1. Calculate its hash at startup
2. Block it if injected (no matter where it's injected from)

---

## 📝 How to Use

### Step 1: Add DLL to This Folder
Copy the DLL you want to blacklist here:
```
blacklisted_dlls/
  ├── OffsetFinder.dll
  ├── cheat.dll
  ├── raax.dll
  └── README.md (this file)
```

### Step 2: Add to Blacklist in dllmain.cpp
```cpp
// In dllmain.cpp, add:
AddDLLToBlacklist(L"blacklisted_dlls\\OffsetFinder.dll");
AddDLLToBlacklist(L"blacklisted_dlls\\cheat.dll");
AddDLLToBlacklist(L"blacklisted_dlls\\raax.dll");
```

### Step 3: Rebuild
- Rebuild the project
- The anticheat will hash these DLLs at startup

---

## ✅ Advantages

1. **Don't need the DLL on your system** - Just put it in this folder
2. **Easy to manage** - All blacklisted DLLs in one place
3. **Portable** - Can distribute with your anticheat
4. **Version control** - Track which DLLs are blacklisted

---

## 🎯 Important Notes

- The DLL will be blocked **no matter where it's injected from**
- Path doesn't matter - only file content (hash) matters
- Renaming doesn't help - hash stays the same
- Moving doesn't help - hash stays the same

---

## 📊 Example

### You have:
```
blacklisted_dlls/OffsetFinder.dll
```

### You add to dllmain.cpp:
```cpp
AddDLLToBlacklist(L"blacklisted_dlls\\OffsetFinder.dll");
```

### Result:
**Blocked everywhere:**
- ✅ `C:\Windows\System32\OffsetFinder.dll`
- ✅ `C:\Users\Desktop\OffsetFinder.dll`
- ✅ `C:\Temp\renamed.dll` (if it's the same file)
- ✅ **ANY location with the same content**
