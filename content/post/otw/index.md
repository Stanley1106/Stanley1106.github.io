---
title: OverTheWire 解題紀錄
description: 手把手解 OverTheWire
slug: overthewire
date: 2024-09-24 00:00:00+0000
image: over-the-wire.png
categories:
    - Hacking
tags:
    - Hacking
    - Linux
    - Note
weight: 1       # You can add weight to some posts to override the default sorting (date descending)
---

# OverTheWire 解題紀錄

## Bandit


## 網址

https://overthewire.org/wargames/bandit/

### Level0

```shell
ssh bandit0@bandit.labs.overthewire.org -p 2220
```
使用此指令連線到此伺服器，輸入密碼 `bandit0` 即可連線。

---

### Level0 -> Level1

先用 `ls` 查看底下的檔案，可以看到 readme 檔，用 `cat` 指令讀取檔案內容。
看到密碼後，就可以 `ctrl + D` 退出伺服器。
:::spoiler Flag
NH2SXQwcBdpmTEzi3bvBHMM9H66vVXjL
:::

---

### Level1 -> Level2

這一題要我們處理非字元符號，剛開始先 `ls` 可以看到檔名為 `-` ，無法直接用 `cat` ，因此我們在 `-` (檔名) 前面加上 `./` (當前目錄)，再用 `cat` 讀取 ，就可以看到密碼了。

:::spoiler Flag
rRGizSaX8Mk1RTb1CNQoXTcYZWU6lgzi
:::

---

### Level2 -> Level3

這題要我們處理名稱內有空格的檔案，放 `\` 在空格前，就可以用 `cat` 讀取。

:::spoiler Flag
aBZ0W5EmUfAf7kHTQeOwd8bauFJ2lAiG
:::

---

### Level3 -> Level4

此提要處理被隱藏的檔案，剛開始先 `cd` 進 `inhere` 資料夾，`ls` 時會發現沒有檔案，這時可以在 `ls` 後加上參數 `-a` 顯示所有檔案(包含隱藏項目)，就看到 `.hidden` 的檔，依樣用 `cat` 就可以拿到密碼了。

:::spoiler Flag
2EW7BBsr6aMMoJ2HjW067dm8EgX26xNe
:::

---

### Level4 -> Level5

剛進去時可以看到 `inhere` 的資料夾，進入後會發戲有10個檔案，題目要我們找到可閱讀的檔案，用 [`file ./*`](https://man7.org/linux/man-pages/man1/file.1.html) 查看底下所有的檔案格式，會發現 `-file07` 是 `ASCII text` 格式，直接`cat` 進去就可以看到密碼。

:::spoiler Flag
lrIWWI6bB37kxfiCQZqUdOIYfr6eEeqR
:::

---

### Level5 -> Level6

進入時直接進入 `inhere` 資料夾，裡面有很多檔案，題目要我們找到1033 bytes in size 的檔案，用 [`find -size 1033c`](https://man7.org/linux/man-pages/man1/find.1.html)，顯示說此檔案位於 `./maybehere07/.file2`，就可以找到密碼了。

:::spoiler Flag
P4L4vucdmLnm8I7Vl7jG1ApGSfjYKqJU
:::

---

### Level6 -> Level7

這題與上一題類似，這次要找的是 *owned by bandit7，group bandit6，33 bytes in size*，因此一樣會用到 [`find`](https://man7.org/linux/man-pages/man1/find.1.html)，輸入 `find -user bandit7 -group bandit6 -size 33c` 後，會發現有許多 `permission denied` ，在原本指令後加上 `2>/dev/null` 將其忽略，就能看到密碼藏在 `/var/lib/dpkg/info/bandit7.password` 中。

:::spoiler Flag
z7WtoNQU2XfjmMtWA8u5rN4vzqu4v99S
:::

---

### Level7 -> Level8

此題要我們找到放在 millionth 旁的密碼，用grep即可找到密碼，輸入 `grep million data.txt`。

:::spoiler Flag
TESKZC0XvTetK0S9xNwm25STk5iWrBvP
:::

---

### Level8 -> Level9


這題要我們尋找在 `data.txt` 裡，只出現一次的密碼，因此我們可以用 `uniq -u` 來查找只出現一次的內容，會發現出現非常多的航數。
```shell=
bandit8@bandit:~$ uniq data.txt
kjIuqjobFBhKw9Mmfj2wAnWbXB2VxSfv
5Y76FifuxKStZi4CVovF2uPhgLrZnLzG
AiYd84lOOVTA4gqJPX7f6DH8eG3zwq1W
A16BW831T94qcsYcGDSkgzYhxnX2xUdK
vlsSKqk3yVx2PZxIkBuZPR3KKIf8hGi1
cEqNrEqHVIIi9fQKdcvAxaip1brmsSxT
FQIgwPiuPKftkFhIy9Nzm94sWdNGTlHd
P8jd7Kr8GXVKTLhe1Y7cVYAARwh4lN4A
Rlaj8VWIHkYsAg42TsFplgAd4ekjgR2X
```
是因為 `uniq` 只抓重複的相鄰行，所以我們可以先將檔案先進行排序 `sort`，最後輸入`sort data.txt | uniq -u` 就能找到此題的 flag。

> `|` 為管線命令，連結前一個命令的**輸出**和下一個命令的**輸入**。

:::spoiler Flag
EN632PlfYiZbn3PhVK3XOGSlNInNE00t
:::

---

### Level9 -> Level10


此題要獲取 `data.txt` 檔案中的 flag 但可以發現到檔案裡是一堆亂碼。

```shell=
bandit9@bandit:~$ cat data.txt
~��Mk���Axڋ��k��;�␦Jb��mi��~�]��]㹩�ux��R~&����4SA&l"����x�     ٗ6m�q���bf��s���~n�����n����
                      ��~��=�|ڱ|J�<��=��u��ڷV���1�`�;�s��g�M-�2k���h�(��1�o�0;T�}��DE*'3�i,���x�ʤ��iSn3�6E�p:���M���O!�d����tW������]��]4&�7�FR^+�6ư�������#
                d��w�'q�Ԇ
                         ��x�)�,V��*"�3��_�3+2)`��5HF���x[
��i�܃�i��}y��M2�3Hu����i�[��U�(�.B�9'�z,
                                        W9�Z��Pf���7A*���f�l�nD}��M��#�~
���=����؇���t6�c���89���⟢V2$�ky�N���    ��ۏ_\��7���q@v���~��%�٣c?G�o��
```

用 `strings data.txt` 指令將檔案內容轉為可讀的字串，就能看到此題的 flag 放在 `=` 的後面。

```shell=
bandit9@bandit:~$ strings data.txt
========== theG)"
========== passwordk^
========== is
========== G7w8LIi6J3kTb8A7j9LgrywtEUlyyp6s
```

:::spoiler Flag
G7w8LIi6J3kTb8A7j9LgrywtEUlyyp6s
:::

---

### Level10 -> Level11

這題要我們用 base64 去解碼 `data.txt` ，使用 `base64` 指令來加密，加上 `-d` 來解碼。

```shell=
bandit10@bandit:~$ base64 data.txt
VkdobElIQmhjM04zYjNKa0lHbHpJRFo2VUdWNmFVeGtVakpTUzA1a1RsbEdUbUkyYmxaRFMzcHdh
R3hZU0VKTkNnPT0K
bandit10@bandit:~$ base64 -d data.txt
The password is 6zPeziLdR2RKNdNYFNb6nVCKzphlXHBM
```

:::spoiler Flag
6zPeziLdR2RKNdNYFNb6nVCKzphlXHBM
:::

### Level11 -> Level12

連線後，`data.txt` 內容為
```shell=
bandit11@bandit:~$ cat data.txt
Gur cnffjbeq vf WIAOOSFzMjXXBC0KoSKBbJ8puQm5lIEi
```

題目要求我們將每個字元 Unicode 編碼差異為 13 解密，可以利用 `tr` 指令轉換字符。

```shell=
bandit11@bandit:~$ cat data.txt |tr "A-Za-z"  "N-ZA-Mn-za-m"
The password is JVNBBFSmZwKKOP0XbFXOoW8chDz5yVRv
```
> "A-Za-z" 舊字串的字元 +13 後為 "N-ZA-Mn-za-m" 的新字串字元。

:::spoiler Flag
JVNBBFSmZwKKOP0XbFXOoW8chDz5yVRv
:::
