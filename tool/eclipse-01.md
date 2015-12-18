>An internal error occurred during: "Requesting JavaScript AST from selection".

##### 原因：
用 Eclipse Helios或者Eclipse indigo 编写Javascript函数中出现 return 时会出现该问题
##### 解决方法：
Window-->Preferences->Javascript-->Editor-->Mark Occurrences
取消选择`mark occurences of the selected element in the current file`