## **Branch**

Branch merupakan suatu percabangan repository di dalam git
``` java
git branch
```
``` java
git branch [--color[=<when>] | --no-color] [--show-current]
	[-v [--abbrev=<length> | --no-abbrev]]
	[--column[=<options>] | --no-column] [--sort=<key>]
	[(--merged | --no-merged) [<commit>]]
	[--contains [<commit]] [--no-contains [<commit>]]
	[--points-at <object>] [--format=<format>]
	[(-r | --remotes) | (-a | --all)]
	[--list] [<pattern>…​]
git branch [--track | --no-track] [-f] <branchname> [<start-point>]
```
![Figure 1](155993572204-gitflow.png)
- Master Branch
  
Master branch Merupakan branch yang sudah siap di rilis atau siap dipakai

- Develop Branch
  
Develop branch merupakan branch yang masih dalam tahap pengembangan oleh programmer

- Feature
  
Merupakan fitur yang sedang dikembangkan oleh programmer

## **Checkout**
`git checkout` merupakan perintah untuk menampilkan *Tree Branch*

#### **Cara menambahkan branch baru**
- Buka branch `git branch`
- Buat branch baru `git checkout -b (namabranchbaru)`
- `git push`
  
## **Merge**
Merge merupakan cara untuk menggabungkan branch tapi sebelum melakukan merge harus melakukan `git checkout` terlebih dahulu ke branch yang mau kita merge

`git checkout (asal) -> git merge (tujuan) -> git push` 

## **Cherry pick**
`git cherry-pick` 

Merupakan perintah untuk menerapkan commit yang didalam nya dapat digunakan kembali

## **Blame**
`git blame` 

Merupakan suatu perintah git untuk mendeteksi aktivitas user

## **Tag**
`git tag`

Merupakan suatu perintah git untuk melabelkan suatu commit

## **Git Ignore**
`gitignore`

merupakan suatu perintah git untuk memilih pengecualian file yang tidak mau ikut tercommit.
Cara membuat file gitignore `touch .gitignore`












