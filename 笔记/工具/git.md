- git 不能add含有中文的文件，原因是git默认是不能识别中文名，需要在终端修改能识别中文才行

  ```bash
  git config --global core.quotepath false
  ```

  `core.quotepath`设为false的话，就不会对`0x80`以上的字符进行quote，中文正常显示

