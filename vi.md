#10 Mẹo để đẩy kỹ năng Git của bạn sang trình độ mới

Gần đây chúng tôi đã ra mắt 2 hướng dẫn giúp bạn làm quen với Git cơ bản và sử dụng Git trong môi trường làm việc nhóm.  Những câu lệnh mà chúng ta thảo luận là đủ để giúp một nhà phát triển thích nghi được trong thế giới Git.Trong bài viết này , Chúng tôi sẽ cố gắng khám phá cách làm thế nào để bạn quản lý thời gian hiệu quaả và sử dụng được đầy đủ tính năng mà Git cung cấp.

Lưu ý: Một vài câu lệnh trong bài viết này bao gồm 1 phần của câu lệnh trong dấu ngoặc vuông (ví dụ. git add -p [file_name]). Trong các ví dụ này, bạn sẽ chèn các số cần thiết, các số nhận dạng , vv . mà không cần dấu ngoặc vuông. 

##1. Tự động hoàn thành Git

Nếu bạn chạy những câu lệnh Git qua dòng lệnh , nó khá là mệt nếu nhập câu lệnh bằng tay ở mọi thời điểm.Để giải quyết vấn đề này , bạn có thể cho phép tự hoàn thành câu lệnh git trong vài phút.

Để có được script, chạy câu lệnh sau ở hệ điều hành Unix:
```
cd ~
curl https://raw.github.com/git/git/master/contrib/completion/git-completion.bash -o ~/.git-completion.bash
```

Sau đó,thêm dòng này ở trong file ```~/.bash_profile``` của bạn:
```
if [ -f ~/.git-completion.bash ]; then
    . ~/.git-completion.bash
fi
```

Mặc dù tôi đã đề cập đến nó khá sớm , Tôi không thể nhấn mạnh nó đủ : Nếu bạn muốn sử dụng các tính năng của Git đầy đủ , bạn chắc chắn nên thay đổi giao diện của dòng lệnh!

##2. Bỏ qua các tệp trong Git

Bạn có mệt mỏi khi các tệp tin biên dịch (như ```.pyc```) xuất hiện trong kho Git của bạn ? hoặc bạn quá ngán khi bạn đã thêm chúng vào Git ? Đừng kiếm ở đâu xa cả , đây chính là một cách qua đó bạn có thể nói với Git để chắc chắn sẽ bỏ qua các tệp và các thư mục hoàn toàn.Đơn giản tạo một tệp với tên ```.gitignore``` và liệt kê các tệp và thư mục mà bạn không muốn Git đánh dấu nó. Bạn có thẻ tạo các ngoại lệ sử dụng dấu cảm thán(!).
```
*.pyc
*.exe
my_db_config/

!main.pyc
```

##3. Ai đã làm rối code của tôi ?

Nó là bản năng tự nhiên của con người chúng ta chỉ trích 1 cái khác khi 1 điều gì đó sai. Nếu máy chủ sản xuất của bạn bị phá vỡ, nó rất dễ dàng để tìm kiếm thủ phạm - chỉ cần thực hiện ```git blame```. Câu lệnh này sẽ hiển thị cho bạn tác giả của mọi dòng lệnh trong file ,commit sẽ thấy được thay đổi cuối cùng của dòng đó , và thời gian của commit đó.

```
git blame [file_name]

```

![ahihi](https://dab1nmslvvntp.cloudfront.net/wp-content/uploads/2014/06/1402946443git-ninja-01.png)

Và trong cái hình ảnh bên dưới , bạn có thể thấy làm thế nào để dòng lệnh có thể nhìn vào 1 repository lớn hơn:

![ahihi](https://dab1nmslvvntp.cloudfront.net/wp-content/uploads/2014/06/1402946441git-ninja-02.png)

##4. Đánh giá lịch sử của repository

Chúng ta đã xem xét việc sử dụng ```git log``` trong cái tutorial trước, tuy nhiên , có 3 lựa chọn mà bạn nên biết đến.

* ```--oneline``` – Nén các thông tin hiển thị trong mỗi commit để giảm bớt các mã hash của commit và thông báo của commit, tất cả được hiển thị trong 1 dòng.
* ```--graph``` – Lựa chọn này vẽ ra một biễu diễn đồ họa dựa trên các ký tự để biểu diễn lịch sửa ở phía tay trái của đầu ra. Nó không được dùng nếu bạn đang xem lịch sử trên một nhánh.
* ```--all``` – HIển thị lịch sử của mọi nhánh.

Đây là kết quả việc hợp các tuỳ chọn ở trên, giống như sau:

![ahihi](https://dab1nmslvvntp.cloudfront.net/wp-content/uploads/2014/06/1402946444git-ninja-03.png)

##5. Không bao giờ để mất theo dõi của một Commit

Hãy nói rằng bạn đã commit 1 cái gì đó bạn không muốn và kết thúc bằng cách thực hiện lại 1 thiết lập khó khăn để trở lại trạng thái trước của bạn. Một lát sau, Bạn nhận ra một vài thông tin khác trong tiến trình và muốn lấy lại nó, hoặc ít nhất là xem nó. Đây là nơi ```git reflog``` có thể giúp.

Một ```git log``` đơn giản hiển thị cho bạn commit cuối cùng, nó là cha mẹ, nó là cha mẹ của cha mẹ, và vân vân. Tuy nhiên, ```git reflog``` là danh sách các commit đầu được chỉ ra. Nhớ rằng nó là cục bộ của hệ thống bạn; Nó không phải 1 phần trong kho của bạn và không bao gồm các pushe và các merger.

Nếu tôi chạy ```git log```, Tôi nhận được các commit đó là một phần của repository của tôi:

![ahihi](https://dab1nmslvvntp.cloudfront.net/wp-content/uploads/2014/06/1402946446git-ninja-04.png)

Tuy nhiên, một ```git reflog``` hiển thị 1 commit (```b1b0ee9 – HEAD@{4}```) mà đã bị một khi bạn thực hiện một thiết lập cứng:

![ahihi](https://dab1nmslvvntp.cloudfront.net/wp-content/uploads/2014/06/1402946447git-ninja-05.png)

##6. Phân loại các phần của 1 tệp đã thay đổi trong 1 Commit

Nói chung, thực tiễn tốt để thực hiện các commit dựa trên tính năng, nghĩa là mỗi commit phải đại diện cho một tính năng hoặc sửa lỗi. Hãy xem xét điều gì sẽ xảy ra nếu bạn cố định hai lỗi hoặc thêm nhiều tính năng mà không thực hiện thay đổi. Trong trường hợp tình hình như vậy, bạn có thể đặt những thay đổi trong một commit duy nhất. Nhưng có một cách tốt hơn: Tập các tập tin riêng lẻ và commit chúng một cách riêng biệt.

Giả sử bạn đã thực hiện nhiều thay đổi trong một tệp và muốn chúng xuất hiện trong các commit riêng biết. Trong trường hợp đó, chúng ta thêm tệp bằng tiền tố ```-p``` thêm vào câu lệnh của chúng ta.

```

git add -p [file_name]

```

Chúng ta hãy cùng nhau chứng minh điều đó. Tôi đã thêm 3 dòng mới vào ```file_name```  và tôi muốn dòng thứ nhất và thứ 3 xuất hiện trong commit của tôi. Hãy xem cài gì mà ```git diff``` cho ta thấy.

![ahihi](https://dab1nmslvvntp.cloudfront.net/wp-content/uploads/2014/06/1402946449git-ninja-06.png)

Và hãy xem điều gì xảy ra khi chúng ta thêm tiền tố ```-p``` vào dòng lệnh ```add``` của chúng ta.

![ahihi](https://dab1nmslvvntp.cloudfront.net/wp-content/uploads/2014/06/1402946450git-ninja-07.png)

Dường như Git giả định rằng tất cả những thay đổi là một phần của cùng ý tưởng, bằng cách nhóm nó vào các khúc đơn.Bạn có các tùy chọn như sau:

* Nhấn y để stage các khúc đó
* Nhấn n nếu không muốn chia các khúc
* Nhấn e để chỉnh sửa các khúc bằng tay
* Nhấn d để thoát hoặc đi đến tệp tiếp theo.
* Nhấn s để phân chia các khúc.

Trong trường hợp của chúng ta, Chúng ta chắc chắn muốn chia chúng thành các phần nhỏ hơn để có chọn lựa điền thêm và loại bỏ phần còn lại.

![ahihi](https://dab1nmslvvntp.cloudfront.net/wp-content/uploads/2014/06/1402946452git-ninja-08.png)

Như bạn có thể thấy, Chúng ta có thể thêm vào đầu và dòng thứ 3 và bỏ đi dòng thứ 2.Bạn có thể xem các tình trạng của kho ngay sau đó và tạo một commit.

![ahihi](https://dab1nmslvvntp.cloudfront.net/wp-content/uploads/2014/06/1402946454git-ninja-09.png)

##7. Squash nhiều Commits

Khi bạn submit code của mình để xem xét và tạo pull request (thường xảy ra trong các dự án mã nguồn mở), bạn có thể được yêu cầu thực hiện thay đổi code của mình trước khi nó được chấp nhận. Bạn thực hiện thay đổi, chỉ để được yêu cầu thay đổi lại nó trong lần xem xét tiếp theo. Trước khi bạn biết nó, bạn có một vài cam kết thêm. Lý tưởng nhất là bạn có thể sử dụng lệnh ```rebase```.

```

git rebase -i HEAD~[number_of_commits]

```

Nếu bạn muốn squash hai commit cuối, lệnh bạn chạy là như sau.

```

git rebase -i HEAD~2

```

Khi chạy lệnh này, bạn được đưa đến một giao diện tương tác liệt kê các commit  và yêu cầu bạn những người nào để squash. Lý tưởng nhận, Bạn ```pick``` commit cuối và ```squash``` cái cũ.

![ahihi](https://dab1nmslvvntp.cloudfront.net/wp-content/uploads/2014/06/1402946455git-ninja-10.png)

Sau đó bạn sẽ yêu cầu cung cấp thông báo commit cho commit mới. quá trình này chủ yếu viết lại lịch sử commit của bạn.

![ahihi](https://dab1nmslvvntp.cloudfront.net/wp-content/uploads/2014/06/1402946457git-ninja-11.png)

##8. Stash các thay đổi chưa được commit

Giả sử bạn đang làm việc trên một lỗi nhất định hoặc một tính năng, và bạn đột nhiên được yêu cầu để chứng minh công việc của bạn. Công việc hiện tại của bạn chưa đủ để commit, và bạn không thể đưa ra một sự thể hiện ở giai đoạn này (mà không quay lại những thay đổi). Trong trường hợp như vậy, ```git stash``` đến để giải cứu. Stash cơ bản thực hiện tất cả các thay đổi của bạn và lưu trữ chúng để sử dụng thêm. Để giấu các thay đổi của bạn, bạn chỉ cần chạy lệnh sau

```

git stash

```

Để kiểm tra danh sách các stash, bạn có thể chạy lệnh sau:

```

git stash list

```

![ahihi](https://dab1nmslvvntp.cloudfront.net/wp-content/uploads/2014/06/1402946458git-ninja-12.png)

Nếu bạn muốn huỷ bỏ stash và phục hồi các thay đổi chưa được commit, bạn áp dụng stash sau:

```

git stash apply

```

Trong ảnh chụp màn hình mới nhất, bạn có thể thấy mỗi stash có một định danh, một số duy nhất (mặc dù chúng ta chỉ có một stash trong trường hợp này). Trong trường hợp bạn muốn áp dụng chỉ các stash chọn lọc, bạn thêm các định danh cụ thể vào câu lệnh ```apply```:

```

git stash apply stash@{2}

```

![ahihi](https://dab1nmslvvntp.cloudfront.net/wp-content/uploads/2014/06/1402946461git-ninja-13.png)


##9. Kiểm tra các Commits bị mất

Mặc dù ```reflog``` là một cách để kiểm tra các commit bị mất, nó không khả thi trong các kho lưu trữ lớn. Đó là khi câu lệnh ```fsck``` (kiểm tra tệp hệ thống) vào cuộc.

```

git fsck --lost-found

```

![ahihi](https://dab1nmslvvntp.cloudfront.net/wp-content/uploads/2014/06/1402946463git-ninja-14.png)

Ở đây bạn có thể thấy một commit bị mất. Bạn có thể kiểm tra các thay đổi trong commit bằng cách chạy ```git show [commit_hash]``` hoặc phục hồi nó bằng cách chạy ```git merge [commit_hash]```.

```git fsck``` có lợi thế hơn ```reflog```.Hãy nói rằng bạn đã xóa một nhánh từ xa và sau đó nhân bản kho. Với ```fsck``` bạn có thể tìm kiếm và phục hồi các nhánh điều khiển đã bị xóa.


##10. Cherry Pick

Tôi đã lưu lệnh Git lịch sự nhất cho lần cuối cùng. Các lệnh ```cherry-pick``` là lệnh Git yêu thích của tôi, bởi vì nó có nghĩa đen cũng như tiện ích của nó!

Trong các điều khoản đơn giản nhất, ```cherry-pick```là chọn một commit duy nhất từ ​​một nhánh khác và kết hợp nó với một nhánh hiện tại. Nếu bạn đang làm việc theo kiểu song song trên hai hoặc nhiều nhánh, bạn có thể nhận thấy một lỗi xảy ra ở tất cả các nhánh. Nếu bạn giải quyết nó trong một, bạn có thể cherry pick các commit vào các nhánh khác, mà không làm phiền với các tập tin  hoặc commit khác.

Hãy xem xét một kịch bản mà chúng ta có thể áp dụng. Tôi có hai nhánh và tôi muốn ```cherry-pick``` the commit ```b20fd14: Cleaned junk``` vào một cái khác.

![ahihi](https://dab1nmslvvntp.cloudfront.net/wp-content/uploads/2014/06/1402946465git-ninja-15.png)

Tôi chuyển sang nhánh mà tôi muốn ```cherry-pick``` the commit, và chạy lệnh sau:

```

git cherry-pick [commit_hash]

```

![ahihi](https://dab1nmslvvntp.cloudfront.net/wp-content/uploads/2014/06/1402946467git-ninja-16.png)

Mặc dù chúng tôi đã có một ```cherry-pick``` thời gian này, bạn nên biết rằng lệnh này thường có thể dẫn đến xung đột, do đó, sử dụng nó cẩn thận.

##Kết luận

Với điều này, chúng ta sẽ đến phần cuối của danh sách các mẹo mà tôi nghĩ rằng có thể giúp bạn nâng cao kỹ năng Git của mình. Git là tốt nhất hiện có và nó có thể hoàn thành bất cứ điều gì bạn có thể tưởng tượng. Vì vậy, luôn luôn cố gắng để thử thách chính mình với Git. Rất có thể, bạn sẽ kết thúc việc học cái gì đó mới!

