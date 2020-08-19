---
title: JS处理移动端虚拟按键影响页面布局
date: 2019-03-20 20:10:39
tags:
---

```
function set_screen(wrap){
	var s_height = document.body.clientHeight; 
	var s_width = document.body.clientWidth;
	var proportion = s_height/s_width;
    if(proportion<1.55){
		var max_warp = document.querySelector(wrap);
    	max_warp.style.height = "37.55" + "rem";
		document.ontouchmove = function(e){
    		...
    	}
    }
}
set_screen(“.wrap”);
```

