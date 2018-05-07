# Meeting-Interface-documentation
Meeting Interface documentation(for FE OA v6.6),建议使用json美化工具查看每个请求/响应的json内容

## 1、会议消息接口

~~1-1、请求会议通知列表：
{
	"iq": {
		"namespace": "MeetingNoticeRequest",
		"query": {
			  "perPageNums": "10", // 每页数量
			  "page":"1", // 页码
		    "searchKey":"" , // 关键字
		    "type":"0"
		}
	}
}~~

~~1-1、响应会议通知列表：
{
	"iq": {
		"namespace": "MeetingNoticeResponse",
		"query": {
		    "totalPage":"1", // 总页数
			  "meetingNoticeList": [{
			      "id":"1000", //会议消息id
				    "name": "讨论吃饭的会议", //会议名
				    "time": "2018:01:22 10:10", //开会时间
				    "state": "0", //参会状态:(2)待定,(1)参加,(0)不参加
				    "initiator": "张三", //会议发起人	
            "deadline": "2018:01:22 10:10", // 会议截止参会时间
			}],
			"errorCode": "0",
			"errorMessage": ""
		}
	}
}~~


#### 4月28日弃用此请求

----

### 1-2、请求会议详情：

<pre><code>
{
	"iq": {
		"namespace": "MeetingNoticeRequest",
		"query": {
			  "id": "1000" ,// 会议消息id
        "msgId": "1000" ,// 消息id
			  "type":"1"
		}
	}
}
</code></pre>

### 1-2、响应会议详情：

<pre><code>
{
	"iq": {
		"namespace": "MeetingNoticeResponse",
		"query": {
		    "id":"1000", // 会议消息id
			  "initiatorId": "9527", // 发起人id
			  "name": "讨论吃饭的会议", // 会议名
			  "initiator": "张三", // 发起人
			  "time": "2018:01:22 10:10", // 会议开始时间
			  "deadline": "2018:01:22 10:10", // 会议截止参会时间
			  "url": "" ,// 表单url
			  "attendNum": 2, // 会议参会人数
			  "notAttendNum": 0, // 会议不参会人数
			  "notDealNum": 12, // 会议未处理人数
			  "meetingUsers": [{
				    "meetingAttendUser": "史玉洁",
				    "meetingAttendStatus": "0"  //参会状态:(2)待定,(1)参加,(0)不参加
			  }], //   会议成员办理情况
			  "repliesList":"[{
			      "sendTime": "2017-09-29 16:57", // 回复时间
			      "sendUser":"张三", // 用户名字
			      "sendUserID":"10", // 用户id
			      "content":"有事不能来" ,// 理由
            "attachments": [ {
               "id": "/v8ANQAxADcANQAy",
               "name": "111.txt",
               "viewName": "111.txt",
               "master_key": "NTE3NTI=",
               "guid": "C6123EE4-B4F2-0442-9F5C-2380EF90D878",
               "width": "",
               "height": "",
               "size": "216.0B",
               "ext_name": "txt_div",
               "type": "10",
               "href": "/servlet/mobileAttachmentServlet?type=0&attachPK=%2Fv8ANQAxADcANQAy"
            }] // 附件
 			  }]",
			"errorCode": "0",
			"errorMessage": ""
		}
	}
}
</pre></code>

---

### 1-3、请求决策是否参会：
<pre><code>
{
	"iq": {
		"namespace": "MeetingNoticeRequest",
		"query": {
         "attachmentGUID": "4f35305b-19b1-4e62-8ab6-4712783f89d1", //  附件的GUID
		     "id":"1000", // 会议消息id
		     "attend":"0" ,// 是否参加会议：（1）参加，（0）不参加
		     "reason":"有事", // 理由 
		     "type":"2"
		}
	}
}
</pre></code>

### 1-3、响应决策是否参会：
<pre><code>
{
	"iq": {
		"namespace": "MeetingNoticeResponse",
		"query": {
			"errorCode": "0",
			"errorMessage": ""
		}
	}
}
</pre></code>

- - - - 

## 2、会议管理接口
### 2-1、请求我参与会议列表：
<pre><code>
{
	"iq": {
		"namespace": "MeetingManageRequest",
		"query": {
			  "perPageNums": "10", // 每页数量
			  "page":"1", // 页码
		      "searchKey":"" , // 关键字
		      "type":"0"
		}
	}
}
</pre></code>

### 2-1、响应我参与会议列表：
<pre><code>
{
	"iq": {
		"namespace": "MeetingManageResponse",
		"query": {
		    "totalPage":"1", // 总页数
			  "meetingList": [{
			      "id":"1000", //会议消息id
				    "name": "讨论吃饭的会议", //会议名
				    "time": "2018:01:22 10:10", //开会时间
				    "state": "0", //开会状态:（2）进行中 （1）待启动 （0）未发布 （3）关闭
				    "address": "南方软件园" //会议地点
			}],
			"errorCode": "0",
			"errorMessage": ""
		}
	}
}
</pre></code>

----

### 2-2、请求会议详情：
<pre><code>
{
	"iq": {
		"namespace": "MeetingManageRequest",
		"query": {
			  "id": "10", // 会议id
        	  "msgId": "1000" ,// 消息id
		     "type":"1"
		}
	}
}
</pre></code>

### 2-2、响应会议详情：
<pre><code>
{
	"iq": {
		"namespace": "MeetingManageResponse",
		"query": {
		    "id":"100", // 会议id
		    "name":"讨论吃饭的会议", // 会议名
		    "time":"2018-01-24 14:54", // 会议开始时间
		    "address":"南方软件园", // 会议地点
		    "host":"李四", // 主持人
		    "attendMember":"张三,李四", // 会议参会人员
            "state":"0" , // //开会状态:（2）启动（进行中） （1）待启动 （0）未发布 （3）关闭
		    "attachments": [{
				"id": "/v8ANQAxADUANwAw",
				"name": "Screenshot_20170613-111037.jpg",
				"viewName": "Screenshot_20170613-111037.jpg",
				"master_key": "NTE1NzA=",
				"guid": "1A718D25-0358-08B8-6911-F035F0D7A750",
				"width": "",
				"height": "",
				"size": "413.82K",
				"ext_name": "jpg_div",
				"time": "",
				"type": "1",
				"href": "/servlet/mobileAttachmentServlet?type=0&attachPK=/v8ANQAxADUANwAw",
			}],
            "summaryAttachments": [{
				"id": "/v8ANQAxADUANwAw",
				"name": "Screenshot_20170613-111037.jpg",
				"viewName": "Screenshot_20170613-111037.jpg",
				"master_key": "NTE1NzA=",
				"guid": "1A718D25-0358-08B8-6911-F035F0D7A750",
				"width": "",
				"height": "",
				"size": "413.82K",
				"ext_name": "jpg_div",
				"time": "",
				"type": "1",
				"href": "/servlet/mobileAttachmentServlet?type=0&attachPK=/v8ANQAxADUANwAw",
			}]， // 会议纪要
                        "agendaList":[{
                        "time":"2018年03月02日15:19", // 发言时间
                        "prolocutor":"张三", // 发言人
                        "content":"讨论吃饭问题"      // 议题          
                        }],
			"errorCode": "0",
			"errorMessage": ""
		}
	}
}
</pre></code>

-----

### 2-3、请求开启（关闭）会议：
<pre><code>
{
	"iq": {
		"namespace": "MeetingManageRequest",
		"query": {
			  "id": "10", // 会议id
			  "method":"2", // 动作 （2）开启 （3）关闭
		      "type":"2"
		}
	}
}
</pre></code>

### 2-3、响应开启（关闭）会议：
<pre><code>
{
	"iq": {
		"namespace": "MeetingManageResponse",
		"query": {
		      "state":"0" , // 状态（1）开启 （0）关闭
			  "errorCode": "0",
			  "errorMessage": ""
		}
	}
}
</pre></code>

-----

### 2-4、请求发布消息：
<pre><code>
{
	"iq": {
		"namespace": "MeetingManageRequest",
		"query": {
			  "id": "10", // 会议id
			  "title":"关于中午集合", // 标题
			  "content":"楼下大操场集合", // 内容
		      "type":"3"
		}
	}
}
</pre></code>

### 2-4、响应发布消息：
<pre><code>
{
	"iq": {
		"namespace": "MeetingManageResponse",
		"query": {
			  "errorCode": "0",
			  "errorMessage": ""
		}
	}
}
</pre></code>

-----

### 2-5、请求会议消息列表：
<pre><code>
{
	"iq": {
		"namespace": "MeetingManageRequest",
		"query": {
		    "searchKey":"", // 关键字（预留）
			  "id": "10", // 会议id
			  "page":"1", // 页码
			  "perPageNums":"10", // 每页数量
		      "type":"4"
		}
	}
}
</pre></code>

### 2-5、响应会议消息列表：
<pre><code>
{
	"iq": {
		"namespace": "MeetingManageResponse",
		"query": {
		      "totalPage":"1", // 总页数
	          "meetingNewsList":[{
	             "newsId":"100", // 消息id
	             "title":"关于中午集合", // 消息标题
	             "content":"大操场集合", // 消息内容
	             "time":"2018-01-24 15:09", // 消息发布时间
	             "publisher":"李四" // 消息发布者
	        }],
			"errorCode": "0",
			"errorMessage": ""
		}
	}
}
</pre></code>

--------

### 2-6、请求我管理会议列表：
<pre><code>
{
	"iq": {
		"namespace": "MeetingManageRequest",
		"query": {
			  "perPageNums": "10", // 每页数量
			  "page":"1", // 页码
		      "searchKey":"" , // 关键字
		      "type":"5"
		}
	}
}
</pre></code>

### 2-6、响应我管理会议列表：
<pre><code>
{
	"iq": {
		"namespace": "MeetingManageResponse",
		"query": {
		    "totalPage":"1", // 总页数
			  "meetingList": [{
			        "id":"1000", //会议消息id
				    "name": "讨论吃饭的会议", //会议名
				    "time": "2018:01:22 10:10", //开会时间
				    "state": "0", //开会状态:（2）进行中 （1）待启动 （0）未发布 （3）关闭
				    "address": "南方软件园" //会议地点
			  }],
			"errorCode": "0",
			"errorMessage": ""
		}
	}
}
</pre></code>

--------

### 2-7、删除消息请求
<pre><code>
{
    "iq": {
        "namespace": "MeetingManageRequest", 
        "query": {
	          "newsId" : "23434",————————消息id
	           "type" : "6"
        }
    }
}
</pre></code>

### 2-7、删除消息响应
<pre><code>
{
    "iq": {
        "namespace": "MeetingManageResponse", 
        "query": {
	            "errorCode": "0",  ———请求成功
            	"errorMessage": ""
        }
    }
}
</pre></code>

------

### 2-8、请求历史会议列表：
<pre><code>
{
	"iq": {
		"namespace": "MeetingManageRequest",
		"query": {
			  "perPageNums": "10", // 每页数量
			  "page":"1", // 页码
		      "searchKey":"" , // 关键字
		      "type":"7"
		}
	}
}
</pre></code>

### 2-8、响应历史会议列表：
<pre><code>
{
	"iq": {
		"namespace": "MeetingManageResponse",
		"query": {
		    "totalPage":"1", // 总页数
			  "meetingList": [{
			        "id":"1000", //会议消息id
				    "name": "讨论吃饭的会议", //会议名
				    "time": "2018:01:22 10:10", //开会时间
				    "allowEnter": "0", //是否允许进入: （0）不允许 （1）允许
				    "address": "南方软件园" //会议地点
			}],
			"errorCode": "0",
			"errorMessage": ""
		}
	}
}
</pre></code>

----


## 3、会议投票接口

### 3.1、发起投票请求
<pre><code>
{
    "iq": {
        "namespace": "MeetingVoteRequest", 
        "query": {
	          "id" : "42343",———————当前会议ID
	          "voteTitle" : "主题",————————-投票标题
	          "voteMultiselect" : "1",——————投票允许多选1.允许，0不允许
	          "voteAnonymous" : 	"1",—————-匿名投票1.允许，0不允许
	          "voteLastTime" : "12小时",—————投票期限(1小时,3小时,6小时,12小时,24小时)	
	          "type" : "0",———请求类型（0.发起投票请求  1.投票列表请求  2.点击确认投票请求  3.点击投票列表请求  4.投票删除请求）
	          “voteOptionArray" : [ ——————— 选项数组 (2~10个选项, 最少2个, 最多10个)
                       		       {
                                 "optionTitle" : "", ——————投票选项1
                                 }, 
		                             {
			                           "optionTitle" : "", ——————投票选项2
                                 },
		                             {
			                           "optionTitle" : "", ——————投票选项3
                                 }
                   			         ]
        }
    }
}
</pre></code>

### 3.1、发起投票响应
<pre><code>
{
    "iq": {
        "namespace": "MeetingVoteResponse", 
        "query": {
	                "errorCode": "0",  ———请求成功
                 	"errorMessage": ""
        }
    }
}
</pre></code>

------

### 3.2、请求投票列表
<pre><code>
{
    "iq": {
        "namespace": "MeetingVoteRequest", 
        "query": {
	          "id" : "42343",——————当前会议ID
	          "perPageNums" : "10",————————每页数量
              "page":"1", ————————页码
	          "searchKey" : "",————————请求关键字
	          "type" : "1",———请求类型（0.发起投票请求  1.投票列表请求  2.点击确认投票请求  3.点击投票列表请求  4.投票删除请求）        }
    }
}
</pre></code>

### 3.2、投票列表响应
<pre><code>
{
	"iq": {
		"namespace": "MeetingVoteResponse",
		"query": {
          "totalPage":"1",————————————总页数
			    "voteList": [{
			    "voteTitle" : "投票标题",——————投票标题
			    "voteId" : "投票ID", ————————投票ID标识
			    "userName" : "用户名", ——————投票发起投票人名字
			    "userId" : "用户ID", ————————投票发起投票人ID
                        "voteDate" : "2017-12-30 10:30“, ——投票日期
                         "voteNumber" : "12", ——————— 已投票人数
                         "voteType" : "0", ———————投票状态(0)未投票 ，(1)已投票，（2）已过期
			    }],
     "errorCode": "0", 
     "errorMessage": ""
		}
	}
}
</pre></code>

---------

### 3.3、点击确认投票请求
<pre><code>
{
    "iq": {
        "namespace": "MeetingVoteRequest", 
        "query": {
	      "voteId" : “23434”,————————投票ID
	      "type" : "2",———请求类型（0.发起投票请求  1.投票列表请求  2.点击确认投票请求  3.点击投票列表请求  4.投票删除请求）
	      "optionId"：""  ——判断是否多是选项（若多选optionId拼接字符串用“，”隔开）
        }
    }
}
</pre></code>

### 3.3、点击确认投票响应
<pre><code>
{
    "iq": {
        "namespace": "MeetingVoteResponse", 
        "query": {
	            "errorCode": "0",  ———请求成功
            	"errorMessage": ""
        }
    }
}
</pre></code>

----------

### 3.4、投票详情请求
<pre><code>
{
    "iq": {
        "namespace": "MeetingVoteRequest", 
        "query": {
	        "voteId" : "23434",————————投票ID
	        "type" : "3",———请求类型（0.发起投票请求  1.投票列表请求  2.点击确认投票请求  3.点击投票列表请求  4.投票删除请求）
        }
    }
}
</pre></code>

### 3.4、投票详情响应
<pre><code>
{
    "iq": {
        "namespace": "MeetingVoteResponse", 
        "query": {
            "resultList": [{
                "voteTitle" : "投票标题",————————投票标题
			    "voteId" : "投票ID", ————————投票ID标识
                "voteNumber" : "12", ——————— 已投票人数
                "voteTotal" : "19", ——————— 投票总人数
		        "voteDate" : "2017-12-30 10:30“, ——投票发起日期
                "voteMultiselect" : "0",——————投票允许多选1.允许，0.不允许
                "voteAnonymous" : 	"1",—————-匿名投票1.允许，0.不允许
                "voteLastDate" : "18:00", ——————投票截止日期
                “voteType”:”1”——————投票状态 1.已投票 0.未投票，2.已过期
                "voteOptionArray": [{
                      "optionId" : "", ———————投票ID
			                "optionTitle" : "", ——————投票选项1
			                "votedNum" : "4", ——————已投票数量
			                "voteJoinArray":[ {
			                "name" : "用户名", ——参与用户名
			                "id" : "用户ID", ————参与投票ID }]
                        }]		
                  }, 
          "errorCode": "0", 
          "errorMessage": ""
        }
    }
}
</pre></code>

--------

### 3.5、投票删除请求
<pre><code>
{
    "iq": {

        "namespace": "MeetingVoteRequest", 
        "query": {
	          "voteId" : "23434",————————投票ID
	           "type" : "4",———请求类型（0.发起投票请求  1.投票列表请求  2.点击确认投票请求  3.点击投票列表请求  4.投票删除请求）
        }
 }
 </pre></code>
    
### 3.5、投票删除请求  
<pre><code>
{
    "iq": {
        "namespace": "MeetingVoteResponse", 
        "query": {
	                "errorCode": "0",  ———请求成功
                 	"errorMessage": ""
        }
    }
}
 </pre></code>
