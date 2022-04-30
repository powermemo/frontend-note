# GIT版本控制

老師的講義\[[連結](http://bryant-huang.gitbook.io/git/fen-zhi-guan-li/jie-jue-chong-tu)]\
安裝很簡單就不放了。

## cmd 指令

每個指令間以空白區隔。\
查詢git版本「`git --version`」

| Mac          | Windows CMD指令 | 說明                     |
| ------------ | ------------- | ---------------------- |
| cd documents | cd documents  | 進入下一層(資料夾)，例如documents |
| ls           | dir           | 查詢資料夾內容                |
|              | cd ..         | 回到上一層                  |

{% hint style="info" %}
mac「command」+「shit」+「.」可以顯示隱藏檔
{% endhint %}

## 打開vs code 終端機

以下是範例操作，我已經有「bash」的情況下，是不用再新建一個「bash」的～。

1\.	Vscode打開後，按下方終端機，在右方下拉是選單按「select default shell」&#x20;

![](<.gitbook/assets/image (46).png>)

2\.	上方會出現下拉選單，點選「Git Bash」&#x20;

![](<.gitbook/assets/image (45).png>)

3\.	再回到下方按下「+」圖案&#x20;

![](<.gitbook/assets/image (48).png>)

## git指令

打在vscode終端機(bash)內。

| 指令                                                | 說明                                                                 |
| ------------------------------------------------- | ------------------------------------------------------------------ |
| `git init`                                        | 將資料夾初始化，建立git儲存庫                                                   |
| `git add .`                                       | <p>批次將子項加入暫存區，<br>「.」可以是指定檔案名稱</p>                                 |
| `git commit -m "可打任何字的註解"`                        | <p>在暫存區到repo間的註解</p><p>(在暫存區才可以加註解，<br>所以跟上面「git add .」是成套的指令)</p> |
| `git reset HEAD`` `_`<file>`_                     | 退出暫存區                                                              |
| `git status`                                      | <p>查看git現在的狀況</p><p>(例如有檔案未加入暫存區，<br>會出現紅色的檔案路徑)</p>               |
| `git log`                                         | 查詢儲存庫紀錄狀態(版號)                                                      |
| `git log --oneline`                               | 列出查詢儲存庫紀錄狀態(版號)(較簡潔)                                               |
| `git checkout 版號`                                 | 回到指定的版號(版本)                                                        |
| `git checkout master`                             | 回到現在(最新)的版號(版本)                                                    |
| `git config --global user.name "github的username"` | 設定識別資料-user name                                                   |
| `git config --global user.email "github的email"`   | 設定識別資料-user email                                                  |
| `git config --list`                               | 查詢識別資料                                                             |

{% hint style="danger" %}
&#x20;切記不要對 c 系統槽做初始化，如果不小心做的，就把 .git 這個檔案刪掉
{% endhint %}

{% hint style="info" %}
修改檔案後才下「`git add .`」「`git commit -m "可打任何字的註解"`」指令
{% endhint %}

{% hint style="info" %}
插播，`git config --list`，不小心進入「git」，輸入「`wq`」退出。\
想了解更多詳情，請查詢「vim指令」。
{% endhint %}

{% hint style="info" %}
檔案修改後，在 source control\*的\
message框\*內 輸入註解文字，就相當於以下兩個指令\
「`git add .`」+「`git commit -m "可打任何字的註解"`」
{% endhint %}

![source control](<.gitbook/assets/image (51).png>)

![message框](<.gitbook/assets/image (54).png>)

## 連線github

步驟一，github新建一個資料夾

![](<.gitbook/assets/image (52).png>)

步驟二，將github產生的指令copy到vscode終端機上貼上，例如：

```
git remote add origin https://github.com/username/132.git
git push -u origin master
```

然後打你的github帳密。

### 插播－GIT密碼打錯怎麼辦？

{% hint style="warning" %}
2020-08-12新增，感覺不是密碼錯誤的問題...而是我瀏覽器用另一個使用者(B)登入，然後VScode讀到(B)的伺服端(?)才會報錯.....。
{% endhint %}

打開「git bash」

![git bash](<.gitbook/assets/image (57).png>)

前面的前置作業「git push –u origin master」\
彈出視窗輸入「user name」「user password」

![git push -u origin master](<.gitbook/assets/image (56).png>)

## github專案加入隊員

1. 到專案內按tab「settings」
2. 左邊tab按「manage access」
3. 下面按「invite a collaborator」   ，打上隊員的user name 例如「roycanfly」「sexfat」

![](<.gitbook/assets/image (49).png>)

## VS code用github互傳檔案

接收邀請後，其他隊員請在本機端建立一個資料夾，打開VS code 輸入github專案的路徑。例如

```
git clone https://github.com/username/132.git
```

![](<.gitbook/assets/image (55).png>)

更新的檔案後，按下vs code左方的圖示「source control」，然後按下打勾確認。

![](<.gitbook/assets/image (47).png>)

然後VScode的左下角訊息就有顯示上傳，記得**手動按下**更新圖示哦～

![](<.gitbook/assets/image (50).png>)

### 分支衝突合併

![](<.gitbook/assets/image (53).png>)

{% hint style="info" %}
&#x20;當改到相同檔案就會有衝突，\
&#x20;**解決的方式： 就是合併完後再重新推上去一版**
{% endhint %}

## git 指令集



```
git init                                       # 初始化本地git倉庫（創建新倉庫）
git config --global user.name "xxx"            # 配置用戶名
git config --global user.email "xxx@xxx.com"   # 配置郵件
git config --global color.ui true              # git status等命令自動著色
git config --global color.status auto
git config --global color.diff auto
git config --global color.branch auto
git config --global color.interactive auto
git config --global --unset http.proxy          # remove proxy configuration on git
git clone git+ssh://git@192.168.53.168/VT.git   # clone遠程倉庫
git status                                      # 查看當前版本狀態（是否修改）
git add xyz                                     # 添加xyz文件至index
git add .                                       # 增加當前子目錄下所有更改過的文件至index
git commit -m 'xxx'                             # 提交
git commit --amend -m 'xxx'                     # 合併上一次提交（用於反復修改）
git commit -am 'xxx'                            # 將add和commit合為一步
git rm xxx                                      # 刪除index中的文件
git rm -r *                                     # 遞歸刪除
git log                                         # 顯示提交日誌
git log -1                                      # 顯示1行日誌 -n為n行
git log -5
git log --stat                                  # 顯示提交日誌及相關變動文件
git show dfb02e6e4f2f7b573337763e5c0013802e392818 # 顯示某個提交的詳細內容
git show dfb02                                  # 可只用commitid的前幾位
git show HEAD                                   # 顯示HEAD提交日誌
git show HEAD^          # 顯示HEAD的父（上一個版本）的提交日誌 ^^為上兩個版本 ^5為上5個版本
git tag                                         # 顯示已存在的tag
git tag -a v2.0 -m 'xxx'                        # 增加v2.0的tag
git show v2.0                                   # 顯示v2.0的日誌及詳細內容
git log v2.0                                    # 顯示v2.0的日誌
git diff                                        # 顯示所有未添加至index的變更
git diff --cached                               # 顯示所有已添加index但還未commit的變更
git diff HEAD^                                  # 比較與上一個版本的差異
git diff HEAD -- ./lib                          # 比較與HEAD版本lib目錄的差異
git diff origin/master..master                  # 比較遠程分支master上有本地分支master上沒有的
git diff origin/master..master --stat           # 只顯示差異的文件，不顯示具體內容
git remote add origin git+ssh://git@192.168.53.168/VT.git # 增加遠程定義（用於push/pull/fetch）
git branch                                      # 顯示本地分支
git branch --contains 50089                     # 顯示包含提交50089的分支
git branch -a                                   # 顯示所有分支
git branch -r                                   # 顯示所有原創分支
git branch --merged                             # 顯示所有已合併到當前分支的分支
git branch --no-merged                          # 顯示所有未合併到當前分支的分支
git branch -m master master_copy                # 本地分支改名
git checkout -b master_copy                     # 從當前分支創建新分支master_copy並檢出
git checkout -b master master_copy              # 上面的完整版
git checkout features/performance               # 檢出已存在的features/performance分支
git checkout --track hotfixes/BJVEP933          # 檢出遠程分支hotfixes/BJVEP933並創建本地跟踪分支
git checkout v2.0                               # 檢出版本v2.0
git checkout -b devel origin/develop            # 從遠程分支develop創建新本地分支devel並檢出
git checkout -- README                          # 檢出head版本的README文件（可用於修改錯誤回退）
git merge origin/master                         # 合併遠程master分支至當前分支
git cherry-pick ff44785404a8e                   # 合併提交ff44785404a8e的修改
git push origin master                          # 將當前分支push到遠程master分支
git push origin :hotfixes/BJVEP933              # 刪除遠程倉庫的hotfixes/BJVEP933分支
git push --tags                                 # 把所有tag推送到遠程倉庫
git fetch                                       # 獲取所有遠程分支（不更新本地分支，另需merge）
git fetch --prune                               # 獲取所有原創分支並清除服務器上已刪掉的分支
git pull origin master                          # 獲取遠程分支master並merge到當前分支
git mv README README2                           # 重命名文件README為README2
git reset --hard HEAD                           # 將當前版本重置為HEAD（通常用於merge失敗回退）
git rebase
git branch -d hotfixes/BJVEP933 # 刪除分支hotfixes/BJVEP933（本分支修改已合併到其他分支）
git branch -D hotfixes/BJVEP933 # 強制刪除分支hotfixes/BJVEP933
git ls-files                                    # 列出git index包含的文件
git show-branch                                 # 圖示當前分支歷史
git show-branch --all                           # 圖示所有分支歷史
git whatchanged                                 # 顯示提交歷史對應的文件修改
git revert dfb02e6e4f2f
```

## 【git flow】\[[link](https://github.com/o0o0o1o0/groupButMy.git)]

## 【緊急】多個GIT帳號切換

\[[**原網址說明**](https://medium.com/@hyWang/907c8eadbabf)]

7.取消Global設定並設定各Repository的User資料\
(若不取消的話，Pull資料時會使用Global的Mail及UserName)\
好像成功？好像失敗....?

```
//取消Global設定
    $git config --global --unset user.name 
    $git config --global --unset user.email

//設定各Repository的User資料
    $git config  user.email "userName@address"     
    $git config  user.name "userName"
```

##
