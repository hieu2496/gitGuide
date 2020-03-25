# Git

## Mục đích chung

* Nắm được khái niệm về GIT
* Các câu lệnh thường xuyên sử dụng trong GIT
* Sử dụng GIT trong công việc hằng ngày

## Hướng dẫn chung

Tài liệu tham khảo:

* [Git Basic (EN)](https://git-scm.com/book/en/v2)
* [Git Magic (VI)](http://www-cs-students.stanford.edu/~blynn/gitmagic/intl/vi/)
* [Atlassian](https://www.atlassian.com/git/tutorials/what-is-version-control)
* [Learn by step](http://gitimmersion.com/lab_01.html)
* [Git Cheatsheet](http://ndpsoftware.com/git-cheatsheet.html)

## Guideline

### 1. Khái niệm về GIT

* VCS là gì? Tại sao cần VCS?
* GIT là một VCS. Điểm khác biệt cơ bản giữa GIT với các VCS khác là gì?
* Ưu điểm của GIT là gì?
* File status lifecycle trong GIT

![File status lifecycle](https://raw.githubusercontent.com/lqtuan/training/master/images/git_file_status_lifecycle.png)
* Local - Remote concepts

![Local - Remote concepts](https://raw.githubusercontent.com/lqtuan/training/master/images/git_local_remote_basic.png)


### 2. Các câu lệnh GIT cơ bản

[Basic Commands](https://www.atlassian.com/git/tutorials/svn-to-git-prepping-your-team-migration/basic-git-commands)

### 3. Git workflow
#### 3.1 Cài đặt git for windows

#### 3.2 Clone code dự án

##### 3.2.1 Lấy remote address của dự án

```
https://github.com/hieu2496/gitGuide.git
```

*Lưu ý: Có thể setting ssh-key để clone code từ địa chỉ dạng "git@github.com:hieu2496/gitGuide.git" để không cần nhập username/password khi thực hiện các tao tác với git (Tham khảo tại [đây](https://help.github.com/articles/generating-ssh-keys/))*

##### 3.2.2 Clone code

Tại thư mục chứa code, chẳng hạn `C:\xampp\htdocs`, gõ lệnh:

```
git clone https://github.com/hieu2496/gitGuide.git training
```
Code của dự án sẽ được clone về thư mục `C:\xampp\htdocs\training`

*Lưu ý: Không truyền training thì mặc định sẽ được clone về thư mục `C:\xampp\htdocs\gitGuide`*


##### 3.2.3 Kiểm tra lại remote

Vào thư mục training. Kiểm tra lại địa chỉ remote

```
git remote -v
```

Nếu kết quả như sau thì việc clone code đã thành công.

```
origin  https://github.com/hieu2496/gitGuide.git (fetch)
origin  https://github.com/hieu2496/gitGuide.git (push)
````

#### 3.3 Cập nhật code

Nên thực hiện kiểm tra tình trạng hiện tại vào đầu giờ sáng, trước khi bắt đầu làm việc hoặc trước khi làm một task mới.

```
git fetch origin
```

Ta sẽ thấy các thay đổi trên hệ thống: các branch mới được tạo, các branch được cập nhật. Ngoài ra lệnh fetch còn cập nhật đồng bộ lại dữ liệu giữa repo local và repo remote.

Trường hợp branch master có thay đổi, cần cập nhật branch bằng lệnh:

```
git pull origin master
```

#### 3.4 Bắt đầu code một redmine issue

##### 3.4.1 Kiểm tra branch master đã được cập nhật hay chưa

Quay về branch master

```
git checkout master
```

Cập nhật origin remote repository

```
git fetch origin
```

Pull code mới nhất từ branch master

```
git pull origin master
```

##### 3.4.2 Tạo branch mới từ branch làm việc (ở đây là master)

*Tuyệt đối không tạo branch làm task từ bất kỳ một branch nào khác, kể cả branch issue có liên quan hoặc issue cha.*

Tạo branch mới

```
git checkout -b tên_branch
```

Quy tắc đặt tên branch mới:

```
feature-RedmineIssuesId-mã_màn_hình-chức_năng_màn_hình
```
*Lưu ý: Tên branch viết hết bằng chữ thường*

Ví dụ:

```
feature-6996-feba010-top-english
```

Trường hợp issue fix bug hoặc issue con từ bất kỳ issue cha nào mà ta đã tạo branch. Tên branch nên được đặt như sau:

```
feature-RedmineIssuesId-mã_màn_hình-lỗi_cần_fix-fixbug
feature-RedmineIssuesId-mã_màn_hình-chức_năng_thêm-enhancement
```

Ví dụ:

```
feture-6996-feba010-reading-recommend-fixbug
```

Một branch chỉ nên viết code để thực hiện một issue. Tránh code nhiều issue trên cùng một branch.

#### 3.5 Tạo commit sau khi code xong

##### 3.5.1 Kiểm tra lại các thay đổi sau khi code

```
git status
```

Ta sẽ nhìn thấy danh sách các file đã thay dổi:

```
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

        modified:   public/js/view.js
        modified:   public/js/view.js.map
        modified:   resources/views/groups/permisions.blade.php
```

Kiểm tra lại các đoạn code đã thay đổi

```
git diff (for all)
git diff tên_file
```

Kết quả nhìn thấy có dạng:

```
diff --git a/public/js/view.js b/public/js/view.js
index a40d16b..74f2570 100644
--- a/public/js/view.js
+++ b/public/js/view.js
@@ -457,110 +457,6 @@ function updateChart(data, options) {
 function changeGroupUserProfileImage() {
     $('.menu-item .avatar').attr('src', $("#new-user-img").attr("src"));
 }
-$(document).ready(function() {
-    //delete manual button
-    $(document).on("click", ".delete-manual-btn", function() {
-        var manualId = $(this).attr("data-manual-id");
-        if (confirm("このマニュアルを削除します。よろしいですか？")) {
-            $('#manual-form-' + manualId).submit();
-        }
-    });
-});
 (function ($) {
 
     var base = {
@@ -1578,6 +1474,110 @@ $(document).ready(function() {
     });
 });
 $(document).ready(function() {
+    //delete manual button
+    $(document).on("click", ".delete-manual-btn", function() {
+        var manualId = $(this).attr("data-manual-id");
+        if (confirm("このマニュアルを削除します。よろしいですか？")) {
+            $('#manual-form-' + manualId).submit();
+        }
+    });
+});
```

Trong đó các dòng có dấu  "-" màu đỏ là các dòng đã bị xóa, các dòng có dấu "+" màu xanh là các dòng đã thêm vào. Bước này là bước kiểm tra cuối cùng xem các thay đổi về code có vấn đề gì ko? Ngoài ra còn kiểm tra các lỗi về coding convention như đặt tên biến, cấu trúc block, dấu cách thừa cuối dòng, ...

##### 3.5.2 Tạo commit

Add các file thay đổi vào commit

```
git add tên_thư_mục
git add tên_file
```

*Sử dụng lệnh `git add .`* nếu muốn add tất cả các file thay đổi

Ví dụ:

```
git add public/js/
git add resources/
```

Trường hợp có các file bị xóa, sử dụng lệnh `git add -u tên_thư_mục` lệnh này sẽ kiểm tra lại các trường hợp đổi tên file, trường hợp file bị xóa hoàn toàn hoặc trường hợp xóa file cùng tên sau đó add file mới vào.

Kiểm tra lại lần cuối các file đã được add vào commit:

```
git status
```

Kết quả hiển thị có dạng:

```
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

        modified:   public/js/view.js
        modified:   public/js/view.js.map
        modified:   resources/views/groups/permisions.blade.php
```

Tạo commit và message commit

```
git commit -m "message"
```

*Chú ý không nên sử dụng lệnh `git commit --amend`, lệnh này sẽ ghi đè commit gần nhất*

##### 3.5.3 Kiểm tra lại commit vừa tạo

Sau khi tạo commit, cần kiểm tra lại commit vừa tạo:

```
git log --oneline -10
```

Kết quả hiển thị có dạng

```
2876587 6996 Fix bug permission page
977da01 Merge branch '4974_delete_js' into 'working'
....
```

Ta sẽ thấy commit vừa tạo cùng với mã hash và message nằm trên đầu của list log.

#### 3.6 Push code lên remote repository

##### 3.6.1 Gộp commit
Một task sẽ chỉ chấp nhận 1 commit duy nhất. Tuy nhiên trong quá trình làm, vì nhiều lí do mà người lập trình sẽ commit nhiều lần lên branch của mình. Chính vì vậy, sau khi đã hoàn thành task, người lập trình cần gộp nhiều commit đó thành 1 commit duy nhất trước khi tạo merge request.

Để xem các `commit` trên branch của bạn, gõ lệnh:
```
git log --oneline -6
```
*Lưu ý: -6 là số lượng commit muốn xem, có thể chọn bất kì giá trị nào bạn muốn.*

Giả sử có các `commit` như sau:
```
8143fbd   Update edit account.
3b4e5ef   Edit account.
b358725   Update export_promotions_data.rb
6d5f68e   Update export_conversion_logs_data.rb
6ea842b   Update export_click_logs_data.rb
ff9d95d   Merge pull request #968 from avc/tmp
```
Muốn gộp 2 commit 8143fbd, 3b4e5ef thành 1 commit, ta gõ lệnh:
```
git rebase -i HEAD~2
```
hoặc
```
git rebase -i b358725
```
Khi đó ta được màn hình như sau:
```
pick b358725 Update edit account.
pick 3b4e5ef   Edit account.
# Rebase 6d5f68e..8143fbd onto 6d5f68e
#
# Commands:
# p, pick = use commit
# r, reword = use commit, but edit the commit message
# e, edit = use commit, but stop for amending
# s, squash = use commit, but meld into previous commit
# f, fixup = like "squash", but discard this commit's log message
# x, exec = run command (the rest of the line) using shell
#
# These lines can be re-ordered; they are executed from top to bottom.
#
# If you remove a line here THAT COMMIT WILL BE LOST.
```
Nếu không muốn sửa `commit message` thì ta sửa:
```
pick b358725 Update edit account.
pick 3b4e5ef   Edit account.
```
thành
```
pick b358725 Update edit account.
f 3b4e5ef   Edit account.
```
sau đó lưu lại.

Nếu muốn sửa `commit message` thì ta sửa thành:
```
r b358725 Update edit account.
f 3b4e5ef   Edit account.
```
sau đó lưu lại, rồi sửa `commit message` và lưu lại `commit message`.

Tới đây việc `rebase` coi như hoàn thành.

Khi `push` code lên server, nếu đã từng `push` code lên server thì khi `push` code lên cần thêm `-f` vào cuối lệnh `push`:
```
git push origin A -f
```

##### 3.6.2 Cập nhật các thay đổi
Trong quá trình code ở branch của mình, có thể code trên server đã được cập nhật (các task khác đã được merged)
Trước khi bạn đưa code của mình lên server để tạo merge thì bạn cần chắc chắn rằng code của mình đã được cập nhật mới nhất. Và khi đó bạn cần rebase code ở branch của mình với branch phát triển trên server (có thể là master).

*Lưu ý: Tuyệt đối không pull origin master từ branch của bạn mà phải rebase*

Rebase là quá trình lấy các thay đổi trên branch origin master (các thay đổi trong code mà người khác đã làm và merge vào code base) vào branch ở local, sau đó đưa commit mà ta vừa tạo lên đầu  commit stack.

###### 3.6.2.1 Xem các cập nhật
```
git fetch origin
```

###### 3.6.2.2 Rebase code với branch phát triển (ở đây là master)
```
git pull --rebase origin master
```

Trường hợp không có conflict (các mã code vừa do người khác đã thay đổi và merge vào code base, vừa do ta đã thay đổi trên local), sẽ có thông báo thành công hiện ra. Trường hợp có conflict ta cần phải thực hiện việc sửa conflict.

Xem các file conflict

```
git status
```

Các file cần sửa conflict sẽ hiển thị ở dạng "Both modified" màu đỏ. Sửa các file này, sau đó `git add` . Cuối cùng gõ lệnh tiếp tục rebase

```
git rebase --continue
```

##### 3.6.3 Push code

```
git push origin tên_branch
```
*Lưu ý: Nếu đã đừng push lên server rồi thì cần thêm tham số -f*

Ví dụ:

```
git push origin feature-6996-feba010-top-english
git push origin feature-6996-feba010-top-english -f
```

#### 3.7 Tạo merge request

## Bài tập

### 1. Tạo tài khoản tại https://gitlab.com
### 2. Tạo repo thực hành các câu lệnh
