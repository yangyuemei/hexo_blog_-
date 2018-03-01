
---
layout: w
title: jquery-ui-jqLoading.js实现Loading转圈圈等待效果
date: 2017-03-17 16:59:55
tags: jquery特效
category:  jquery特效

---

## 步骤如下

* ### 引入jquery.js 和 jquery-ui-jqLoading.js
* ### 在html文件中给按钮一个id
* ### 写js脚本

___以下为实现代码___

index.html
```javascript
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>转圈圈效果</title>
</head>
<body>
<input type="button" id="btnOpen2" value="转圈圈" />
<script src="https://apps.bdimg.com/libs/jquery/2.1.4/jquery.min.js"></script>
<script src="jquery-ui-jqLoding.js"></script>
<script type="text/javascript">
    $(function () {
        $("#btnOpen2").on("click", function () {
            $.fn.jqLoading({ height: 100, width: 240, text: "正在上传中，请耐心等待...." });
            setTimeout(function () {
                $.fn.jqLoading("destroy");
            }, 3000);
        });
    })
</script>
</body>
</html>
```