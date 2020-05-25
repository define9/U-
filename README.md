# U-校园
U校园部分试题答案（目前只测试过 新标准 综合教程3）
新标准大学英语（第二版）综合3 测试  查看答案
进入test页面后 等待3秒出现  答 案  按钮

教程:未更新

效果:
![avatar][base64str]

代码:
```
// ==UserScript==
// @name         U校园-综合教程3 test
// @namespace    QQ:2066561288
// @version      0.1
// @description  try to take over the world!
// @author       define_9247
// @match        *://u.unipus.cn/user/student/homework/index*
// @match        *://uexercise.unipus.cn/*
// @grant        none
// @require      https://cdn.staticfile.org/jquery/3.3.1/jquery.min.js
// @grant        unsafeWindow
// ==/UserScript==

//let $ = unsafeWindow.jQuery



(function() {
	'use strict';
	window.onload = function(){
		var n = 0;//第二份试题
		var localUrl = window.location.href;
		var courseId = localUrl.match(/courseId=\d+/g);
		var school_id = localUrl.match(/school_id=\d+/g);
		var eccId = localUrl.match(/eccId=\d+/g);
		var classId = localUrl.match(/classId=\d+/g);
		//获取list中
		var stu_id = "";
		var homework_id = "";
		var sign = "";
		var listUrl = "https://u.unipus.cn/user/student/homework/list?length=10&"+school_id+"&"+courseId+"&"+eccId+"&"+classId+"&type=2&state=";
		$.getJSON(listUrl,function(data){
			stu_id = data.rs.list[n].stu_id;
			homework_id = data.rs.list[n].homework_id;
		});
		setTimeout(function(){//延时2s
			//获取forwardUrl
			var schoolId = school_id[0].replace(/[^0-9]/ig,"");
			var clsId = classId[0].replace(/[^0-9]/ig,"");
			var studentId = stu_id;
			var exerciseId = homework_id;
			//获取sign
			var signUrl = "https://u.unipus.cn/user/student/homework/chk?homeworkId="+homework_id+"&"+classId;
			$.getJSON(signUrl,function(data){
				sign = data.rs.sign;
				var tempUrl = "https://uexercise.unipus.cn/uexercise/api/v1/enter_check_student_exam_detail?plf=0&schoolId="+schoolId+"&clsId="+clsId+"&studentId="+studentId+"&exerciseId="+exerciseId;
				var lxforwardUrl = encodeURIComponent(tempUrl);
				var endUrl = tempUrl + "&forwardUrl=" + lxforwardUrl + "&exerciseType=2&sign=" + sign;
				var btn1 = '<a id="lxx" href="javascript:void(0)")">查看答案</button>';
				var body = document.getElementById("tbody");
				var btn = body.getElementsByClassName("last");
				btn[n].innerHTML += btn1;
				var endBtn = document.getElementById("lxx");
				endBtn.onclick = function(){
					window.open(endUrl);
				};
			});
		},"2000");
	};
})();
```
[base64str]:data:image/png;base64,b'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'
