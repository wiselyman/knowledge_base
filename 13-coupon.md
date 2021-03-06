## 说明 
### 券分类
#### 免费券
- `type`: 1
- `freeHours`: 免费时长
- `示例`:

```json
{
    "type":1,
    "freeHours":2
}
```
- `示例说明`: 免费停车两个小时，两小时内不收费
         
#### 小时券
- `type`: 2
- `useLimitHour`: 停车小时数使用限制，停车满指定小时数可用
- `payAmount`: 实付金额(分)
- `示例`:

```json
{
    "type":2,
    "useLimitHour": 2,
    "payAmount": 2000
}
```
- `示例说明`: 2小时收费2元

#### 满减券
- `type`: 3
- `useLimitAmount`: 金额使用限制(分)
- `discountAmount`: 优惠金额(分)
- `示例`:

```json
{
    "type":3,
    "useLimitAmount": 5000,
    "discountAmount": 2000
}
```
- `示例说明`: 满5元减2元   
         
#### 直减券
- `type`: 4
- `discountAmount`: 优惠金额(分)
- `示例`:

```json
{
    "type":4,
    "discountAmount": 2000
}
```
- `示例说明`: 减2元

### 常量

#### 活动状态
- `status`: 1为可用，2为禁用

#### 优惠券状态
- `status`: 1为未发放, 2为未使用, 3为已使用, 4为已失效

#### 优惠券类型
- `type`: 1为免费券, 2为小时券, 3为满减券, 4为直减券

#### 活动所属平台
- `platform`: 1为APP

#### 优惠券领取渠道
-`origin`: 1为APP, 2为H5，3为第三方，4为系统分配，5为手动分配

  
         
## 13.1 优惠活动信息访问接口

### 13.1.1 save接口

- 功能描述: 创建新活动

- 请求地址: `http://domain/coupon/activities`

- 请求动作: `POST`

- 请求示例: `http://localhost:8080/coupon/activities?access_token=9e245715-aef8-47ff-bf4a-3030d6258e03`

- 请求示例

```
{
	"name":"中秋优惠",
	"platform":1 // 活动所属平台, APP活动为1, 非必填参数
	"fullCouponTemplate":{
		"name":"满减券",
		"validStartDate":"2017-11-21 10:30:30",
		"validEndDate":"2017-11-25 10:30:30",
		"roadSections":[],
		"isWholeRoadSection":true, // 是否是全路段
		"couponRules":[
			{
				"type":"3",
				"useLimitAmount":5,
				"discountAmount":2,
				"maxNum":2	
			},
			{
				"type":"3",
				"useLimitAmount":10,
				"discountAmount":5,
				"maxNum":2	
			}
			
		]
	},
	"freeCouponTemplate":{
		"name":"免费券",
		"validStartDate":"2017-11-21 19:30:30",
		"validEndDate":"2017-11-24 12:30:30",
		"roadSections":[{
		  "id":1001,
		  "name":"植保路"
		},{
		  "id":1002,
		  "name":"长江路"
		}],
		"isWholeRoadSection":false,
		"couponRules":[
			{
				"type":"1",
				"freeHours":2,
				"maxNum":2	
			}
		]
	},
	"hourCouponTemplate":{
		"name":"小时券",
		"validStartDate":"2017-11-21 10:30:30",
		"validEndDate":"2017-11-25 10:30:30",
		"roadSections":[{
		  "id":1001,
		  "name":"植保路"
		},{
		  "id":1002,
		  "name":"长江路"
		}],
		"isWholeRoadSection":false,
		"couponRules":[
			{
				"type":"2",
				"useLimitHour":1,
				"payAmount":1,
				"maxNum":2	
			},{
				"type":"2",
				"useLimitHour":2,
				"payAmount":5,
				"maxNum":2	
			}
		]
	},
	"straightCutCouponTemplate":{
		"name":"直减券",
		"validStartDate":"2017-11-21 10:30:30",
		"validEndDate":"2017-11-25 10:30:30",
		"roadSections":[{
		  "id":1001,
		  "name":"植保路"
		},{
		  "id":1002,
		  "name":"长江路"
		}],
		"isWholeRoadSection":false,
		"couponRules":[
			{
				"type":"4",
				"discountAmount":5,
				"maxNum":1	
			},{
				"type":"4",
				"discountAmount":10,
				"maxNum":2	
			}
		]
	},
	"status":1
}

```

### 13.1.2 list接口

- 功能描述: 创建优惠券时，输入活动名获得活动下拉框提醒

- 请求地址: `http://localhost:8080/coupon/activities`

- 请求动作: `GET`

- 请求示例: `http://localhost:8080/coupon/activities?access_token=69ff3003-dee1-40d5-a36f-c0c4fa55c431`

- 返回示例

```
{
    "status": "SUCCESS",
    "data": {
        "content": [
            {
                "id": "5a13cc956c79211554a7f9ca",
                "name": "圣诞优惠",
                "status": 1,
                "fullCouponTemplate": {
                    "name": "满减券",
                    "validStartDate": "2017-11-21 10:30:30",
                    "validEndDate": "2017-11-25 10:30:30",
                    "roadSections": [{
                      "id":1001,
                      "name":"植保路"
                    },{
                      "id":1002,
                      "name":"长江路"
                    }],
                    "isWholeRoadSection":false,
                    "couponRules": [
                        {
                            "type": "3",
                            "useLimitAmount": 5,
                            "discountAmount": 2,
                            "generateNum": null,
                            "maxNum": 2
                        },
                        {
                            "type": "3",
                            "useLimitAmount": 10,
                            "discountAmount": 5,
                            "generateNum": null,
                            "maxNum": 2
                        }
                    ]
                },
                "freeCouponTemplate": {
                    "name": "免费券",
                    "validStartDate": "2017-11-21 19:30:30",
                    "validEndDate": "2017-11-24 12:30:30",
                    "roadSections": [{
                      "id":1001,
                      "name":"植保路"
                    },{
                      "id":1002,
                      "name":"长江路"
                    }],
                    "isWholeRoadSection":false,
                    "couponRules": [
                        {
                            "type": "1",
                            "freeHours": 2,
                            "generateNum": null,
                            "maxNum": 2
                        }
                    ]
                },
                "hourCouponTemplate": {
                    "name": "小时券",
                    "validStartDate": "2017-11-21 10:30:30",
                    "validEndDate": "2017-11-25 10:30:30",
                    "roadSections": [{
                      "id":1001,
                      "name":"植保路"
                    },{
                      "id":1002,
                      "name":"长江路"
                    }],
                    "isWholeRoadSection":false,
                    "couponRules": [
                        {
                            "type": "2",
                            "useLimitHour": 1,
                            "payAmount": 1,
                            "generateNum": null,
                            "maxNum": 2
                        },
                        {
                            "type": "2",
                            "useLimitHour": 2,
                            "payAmount": 5,
                            "generateNum": null,
                            "maxNum": 2
                        }
                    ]
                },
                "straightCutCouponTemplate": {
                    "name": "直减券",
                    "validStartDate": "2017-11-21 10:30:30",
                    "validEndDate": "2017-11-25 10:30:30",
                    "roadSections": [{
                      "id":1001,
                      "name":"植保路"
                    },{
                      "id":1002,
                      "name":"长江路"
                    }],
                    "isWholeRoadSection":false
                    "couponRules": [
                        {
                            "type": "4",
                            "discountAmount": 5,
                            "generateNum": null,
                            "maxNum": 1
                        },
                        {
                            "type": "4",
                            "discountAmount": 10,
                            "generateNum": null,
                            "maxNum": 2
                        }
                    ]
                },
                "createdDate": "2017-11-21 14:49:57"
            }
        ]
    }
}

```
### 13.1.3 search接口

- 功能描述: 活动列表条件查询时

- 请求地址: `http://domain/coupon/activities/search`

- 请求动作: `GET`

- 请求示例: `http://localhost:8080/coupon/activities/search?name=&status=1&page=0&size=2&access_token=69ff3003-dee1-40d5-a36f-c0c4fa55c431&sort=createdDate,DESC`

- 返回示例

sort:createdDate,DESC 按照活动创建时间降序排列

```
{
    "status": "SUCCESS",
    "data": {
        "content": [
            {
                "id": "5a24af70e8452f2734f0e20d",
                "name": "最终优惠",
                "status": null,
                "fullCouponTemplate": {
                    "name": "满减券",
                    "validStartDate": "2017-11-21 10:30:30",
                    "validEndDate": "2017-11-25 10:30:30",
                    "roadSections": [],
                    "isWholeRoadSection": true,
                    "couponRules": [
                        {
                            "type": 3,
                            "useLimitAmount": 5,
                            "discountAmount": 2,
                            "generateNum": null,
                            "maxNum": 2
                        },
                        {
                            "type": 3,
                            "useLimitAmount": 10,
                            "discountAmount": 5,
                            "generateNum": null,
                            "maxNum": 2
                        }
                    ]
                },
                "freeCouponTemplate": {
                    "name": "免费券",
                    "validStartDate": "2017-11-21 19:30:30",
                    "validEndDate": "2017-11-24 12:30:30",
                    "roadSections": [
                        {
                            "id": 1001,
                            "name": "植保路"
                        },
                        {
                            "id": 1002,
                            "name": "长江路"
                        }
                    ],
                    "isWholeRoadSection": false,
                    "couponRules": [
                        {
                            "type": 1,
                            "freeHours": 2,
                            "generateNum": null,
                            "maxNum": 2
                        }
                    ]
                },
                "hourCouponTemplate": {
                    "name": "小时券",
                    "validStartDate": "2017-11-21 10:30:30",
                    "validEndDate": "2017-11-25 10:30:30",
                    "roadSections": [
                        {
                            "id": 1001,
                            "name": "植保路"
                        },
                        {
                            "id": 1002,
                            "name": "长江路"
                        }
                    ],
                    "isWholeRoadSection": false,
                    "couponRules": [
                        {
                            "type": 2,
                            "useLimitHour": 1,
                            "payAmount": 1,
                            "generateNum": null,
                            "maxNum": 2
                        },
                        {
                            "type": 2,
                            "useLimitHour": 2,
                            "payAmount": 5,
                            "generateNum": null,
                            "maxNum": 2
                        }
                    ]
                },
                "straightCutCouponTemplate": {
                    "name": "直减券",
                    "validStartDate": "2017-11-21 10:30:30",
                    "validEndDate": "2017-11-25 10:30:30",
                    "roadSections": [
                        {
                            "id": 1001,
                            "name": "植保路"
                        },
                        {
                            "id": 1002,
                            "name": "长江路"
                        }
                    ],
                    "isWholeRoadSection": false,
                    "couponRules": [
                        {
                            "type": 4,
                            "discountAmount": 5,
                            "generateNum": null,
                            "maxNum": 1
                        },
                        {
                            "type": 4,
                            "discountAmount": 10,
                            "generateNum": null,
                            "maxNum": 2
                        }
                    ]
                },
                "platform": 1
            },
            {
                "id": "5a24ac3e5af9171b67eecb66",
                "name": "中秋优惠",
                "status": 1,
                "fullCouponTemplate": {
                    "name": "满减券",
                    "validStartDate": "2017-11-21 10:30:30",
                    "validEndDate": "2017-11-25 10:30:30",
                    "roadSections": [],
                    "isWholeRoadSection": true,
                    "couponRules": [
                        {
                            "type": 3,
                            "useLimitAmount": 5,
                            "discountAmount": 2,
                            "generateNum": null,
                            "maxNum": 2
                        },
                        {
                            "type": 3,
                            "useLimitAmount": 10,
                            "discountAmount": 5,
                            "generateNum": null,
                            "maxNum": 2
                        }
                    ]
                },
                "freeCouponTemplate": {
                    "name": "免费券",
                    "validStartDate": "2017-11-21 19:30:30",
                    "validEndDate": "2017-11-24 12:30:30",
                    "roadSections": [
                        {
                            "id": 1001,
                            "name": "植保路"
                        },
                        {
                            "id": 1002,
                            "name": "长江路"
                        }
                    ],
                    "isWholeRoadSection": false,
                    "couponRules": [
                        {
                            "type": 1,
                            "freeHours": 2,
                            "generateNum": null,
                            "maxNum": 2
                        }
                    ]
                },
                "hourCouponTemplate": {
                    "name": "小时券",
                    "validStartDate": "2017-11-21 10:30:30",
                    "validEndDate": "2017-11-25 10:30:30",
                    "roadSections": [
                        {
                            "id": 1001,
                            "name": "植保路"
                        },
                        {
                            "id": 1002,
                            "name": "长江路"
                        }
                    ],
                    "isWholeRoadSection": false,
                    "couponRules": [
                        {
                            "type": 2,
                            "useLimitHour": 1,
                            "payAmount": 1,
                            "generateNum": null,
                            "maxNum": 2
                        },
                        {
                            "type": 2,
                            "useLimitHour": 2,
                            "payAmount": 5,
                            "generateNum": null,
                            "maxNum": 2
                        }
                    ]
                },
                "straightCutCouponTemplate": {
                    "name": "直减券",
                    "validStartDate": "2017-11-21 10:30:30",
                    "validEndDate": "2017-11-25 10:30:30",
                    "roadSections": [
                        {
                            "id": 1001,
                            "name": "植保路"
                        },
                        {
                            "id": 1002,
                            "name": "长江路"
                        }
                    ],
                    "isWholeRoadSection": false,
                    "couponRules": [
                        {
                            "type": 4,
                            "discountAmount": 5,
                            "generateNum": null,
                            "maxNum": 1
                        },
                        {
                            "type": 4,
                            "discountAmount": 10,
                            "generateNum": null,
                            "maxNum": 2
                        }
                    ]
                },
                "platform": 1
            }
        ],
        "last": false,
        "totalPages": 2,
        "totalElements": 4,
        "number": 0,
        "size": 2,
        "sort": [
            {
                "direction": "DESC",
                "property": "createdDate",
                "ignoreCase": false,
                "nullHandling": "NATIVE",
                "ascending": false,
                "descending": true
            }
        ],
        "first": true,
        "numberOfElements": 2
    }
}

```

### 13.1.4 web端根据活动id查询活动信息

- 功能描述: 查询活动信息

- 请求地址: `http://domain/coupon/activities/`

- 请求动作: `GET`

- 请求示例: `localhost:8080/coupon/activities/5a1fd3abdcd5d30a33b13256?access_token=69ff3003-dee1-40d5-a36f-c0c4fa55c431`

- 返回示例

```
{
    "status": "SUCCESS",
    "data": {
        "id": "5a1fd3abdcd5d30a33b13256",
        "name": "中秋优惠",
        "status": 1,
        "fullCouponTemplate": {
            "name": "满减券",
            "validStartDate": "2017-11-21 10:30:30",
            "validEndDate": "2017-11-25 10:30:30",
            "roadSections": [],
            "isWholeRoadSection": true,
            "couponRules": [
                {
                    "type": 3,
                    "useLimitAmount": 5,
                    "discountAmount": 2,
                    "generateNum": null,
                    "maxNum": 2
                },
                {
                    "type": 3,
                    "useLimitAmount": 10,
                    "discountAmount": 5,
                    "generateNum": null,
                    "maxNum": 2
                }
            ]
        },
        "freeCouponTemplate": {
            "name": "免费券",
            "validStartDate": "2017-11-21 19:30:30",
            "validEndDate": "2017-11-24 12:30:30",
            "roadSections": [
                {
                    "id": 1001,
                    "name": "植保路"
                },
                {
                    "id": 1002,
                    "name": "长江路"
                }
            ],
            "isWholeRoadSection": false,
            "couponRules": [
                {
                    "type": 1,
                    "freeHours": 2,
                    "generateNum": null,
                    "maxNum": 2
                }
            ]
        },
        "hourCouponTemplate": {
            "name": "小时券",
            "validStartDate": "2017-11-21 10:30:30",
            "validEndDate": "2017-11-25 10:30:30",
            "roadSections": [
                {
                    "id": 1001,
                    "name": "植保路"
                },
                {
                    "id": 1002,
                    "name": "长江路"
                }
            ],
            "isWholeRoadSection": false,
            "couponRules": [
                {
                    "type": 2,
                    "useLimitHour": 1,
                    "payAmount": 1,
                    "generateNum": null,
                    "maxNum": 2
                },
                {
                    "type": 2,
                    "useLimitHour": 2,
                    "payAmount": 5,
                    "generateNum": null,
                    "maxNum": 2
                }
            ]
        },
        "straightCutCouponTemplate": {
            "name": "直减券",
            "validStartDate": "2017-11-21 10:30:30",
            "validEndDate": "2017-11-25 10:30:30",
            "roadSections": [
                {
                    "id": 1001,
                    "name": "植保路"
                },
                {
                    "id": 1002,
                    "name": "长江路"
                }
            ],
            "isWholeRoadSection": false,
            "couponRules": [
                {
                    "type": 4,
                    "discountAmount": 5,
                    "generateNum": null,
                    "maxNum": 1
                },
                {
                    "type": 4,
                    "discountAmount": 10,
                    "generateNum": null,
                    "maxNum": 2
                }
            ]
        },
        "platform": null
    }
}
```

### 13.1.5 web端修改活动信息

- 功能描述: 修改活动信息

- 请求地址: `http://domain/coupon/activities`

- 请求动作: `PUT`

- 请求示例: `localhost:8080/coupon/activities/5a13cc956c79211554a7f9ca?access_token=69ff3003-dee1-40d5-a36f-c0c4fa55c431`

- 请求示例

```
{

		"name":"修改圣诞优惠",
		"status":1,
		 "fullCouponTemplate": {
                "name": "满减券",
                "validStartDate": "2017-11-21 10:30:30",
                "validEndDate": "2017-11-25 10:30:30",
                "roadSections": [{
                  "id":1001,
                  "name":"植保路"
                },{
                  "id":1002,
                  "name":"长江路"
                }],
                "isWholeRoadSection":false,
                "couponRules": [
                    {
                        "type": "3",
                        "useLimitAmount": 5,
                        "discountAmount": 2,
                        "generateNum": 20,
                        "maxNum": 2
                    },
                    {
                        "type": "3",
                        "useLimitAmount": 10,
                        "discountAmount": 5,
                        "generateNum": 20,
                        "maxNum": 2
                    }
                ]
            },
            "freeCouponTemplate": {
                "name": "免费券",
                "validStartDate": "2017-11-21 19:30:30",
                "validEndDate": "2017-11-24 12:30:30",
                "roadSections": [{
                  "id":1001,
                  "name":"植保路"
                },{
                  "id":1002,
                  "name":"长江路"
                }],
                "isWholeRoadSection":false,
                "couponRules": [
                    {
                        "type": "1",
                        "freeHours": 2,
                        "generateNum": 20,
                        "maxNum": 2
                    }
                ]
            },
            "hourCouponTemplate": {
                "name": "小时券",
                "validStartDate": "2017-11-21 10:30:30",
                "validEndDate": "2017-11-25 10:30:30",
                "roadSections": [{
                  "id":1001,
                  "name":"植保路"
                },{
                  "id":1002,
                  "name":"长江路"
                }],
                "isWholeRoadSection":false,
                "couponRules": [
                    {
                        "type": "2",
                        "useLimitHour": 1,
                        "payAmount": 1,
                        "generateNum": null,
                        "maxNum": 2
                    },
                    {
                        "type": "2",
                        "useLimitHour": 2,
                        "payAmount": 5,
                        "generateNum": 20,
                        "maxNum": 2
                    }
                ]
            },
            "straightCutCouponTemplate": {
                "name": "直减券",
                "validStartDate": "2017-11-21 10:30:30",
                "validEndDate": "2017-11-25 10:30:30",
                "roadSections": [{
                  "id":1001,
                  "name":"植保路"
                },{
                  "id":1002,
                  "name":"长江路"
                }],
                "isWholeRoadSection":false,
                "couponRules": [
                    {
                        "type": "4",
                        "discountAmount": 5,
                        "generateNum": 20,
                        "maxNum": 1
                    },
                    {
                        "type": "4",
                        "discountAmount": 10,
                        "generateNum": 20,
                        "maxNum": 2
                    }
                ]
            }
		
}

```

### 13.1.6 app端查询最新可用的活动接口

- 功能描述: 查询最新活动

- 请求地址: `http://domain/coupon/activities/latest`

- 请求动作: `GET`

- 请求示例: `localhost:8080/coupon/activities/latest?access_token=a2ca8f93-209f-433e-a710-065035a340fe&platform=1`

- 返回示例

```

platform:1 app平台

{
    "status": "SUCCESS",
    "data": {
        "id": "5a24ac3e5af9171b67eecb66",
        "name": "中秋优惠",
        "rules": [
            {
                "type": 1,
                "freeHours": 2,
                "generateNum": null,
                "maxNum": 2
            },
            {
                "type": 3,
                "useLimitAmount": 5,
                "discountAmount": 2,
                "generateNum": null,
                "maxNum": 2
            },
            {
                "type": 3,
                "useLimitAmount": 10,
                "discountAmount": 5,
                "generateNum": null,
                "maxNum": 2
            },
            {
                "type": 2,
                "useLimitHour": 1,
                "payAmount": 1,
                "generateNum": null,
                "maxNum": 2
            },
            {
                "type": 2,
                "useLimitHour": 2,
                "payAmount": 5,
                "generateNum": null,
                "maxNum": 2
            },
            {
                "type": 4,
                "discountAmount": 5,
                "generateNum": null,
                "maxNum": 1
            },
            {
                "type": 4,
                "discountAmount": 10,
                "generateNum": null,
                "maxNum": 2
            }
        ]
    }
}

```




## 13.2 优惠券信息访问接口


### 13.2.1 web端新增优惠券接口

- 功能描述: 新增优惠券

- 请求地址: `http://domain/coupon/coupons`

- 请求动作: `POST`

- 请求示例: `http://localhost:8080/coupon/coupons?access_token=69ff3003-dee1-40d5-a36f-c0c4fa55c431`

- 请求示例

```
 {
  "activity":{
   "id":"5a13cc956c79211554a7f9ca",
   "name":"圣诞优惠"
  },
  "fullCouponTemplate":{
   "name":"满减券",
   "validStartDate":"2017-11-21 10:30:30",
   "validEndDate":"2017-11-24 10:30:30",
   "roadSections": [{
     "id":1001,
     "name":"植保路"
   },{
     "id":1002,
     "name":"长江路"
   }],
   "isWholeRoadSection":false,
   "couponRules":[
    {
     "type":"3",
     "useLimitAmount":5,
     "discountAmount":2,
     "maxNum":2,
     "generateNum":5
    },
    {
     "type":"3",
     "useLimitAmount":10,
     "discountAmount":5,
     "maxNum":2,
     "generateNum":5 
    }
    
   ]
  },
  "freeCouponTemplate":{
   "name":"免费券",
   "validStartDate":"2017-11-21 19:30:30",
   "validEndDate":"2017-11-24 12:30:30",
   "roadSections": [{
     "id":1001,
     "name":"植保路"
   },{
     "id":1002,
     "name":"长江路"
   }],
   "isWholeRoadSection":false,
   "couponRules":[
    {
     "type":"1",
     "freeHours":2,
     "maxNum":2,
     "generateNum":5 
    }
   ]
  },
  "hourCouponTemplate":{
   "name":"小时券",
   "validStartDate":"2017-11-21 10:30:30",
   "validEndDate":"2017-11-24 10:30:30",
   "roadSections": [{
     "id":1001,
     "name":"植保路"
   },{
     "id":1002,
     "name":"长江路"
   }],
   "isWholeRoadSection":false,
   "couponRules":[
    {
     "type":"2",
     "useLimitHour":1,
     "payAmount":1,
     "maxNum":2,
     "generateNum":5 
    },{
     "type":"2",
     "useLimitHour":2,
     "payAmount":5,
     "maxNum":2,
     "generateNum":5 
    }
   ]
  },
  "straightCutCouponTemplate":{
   "name":"直减券",
   "validStartDate":"2017-11-21 10:30:30",
   "validEndDate":"2017-11-24 10:30:30",
   "roadSections": [{
     "id":1001,
     "name":"植保路"
   },{
     "id":1002,
     "name":"长江路"
   }],
   "isWholeRoadSection":false,
   "couponRules":[
    {
     "type":"4",
     "discountAmount":5,
     "maxNum":1,
     "generateNum":5
    },{
     "type":"4",
     "discountAmount":10,
     "maxNum":2,
     "generateNum":5
    }
   ]
  },
  "phoneNums":[],
  "assignable":true
 }


```

### 13.2.4 web端给优惠券分配手机号

- 功能描述: 分配优惠券

- 请求地址: `http://domain/coupon/coupons`

- 请求动作: `PUT`

- 请求示例: `localhost:8080/coupon/coupons/assignCoupon?access_token=69ff3003-dee1-40d5-a36f-c0c4fa55c431&id=586adbde-3877-4397-a1fa-19e40aa97d39&phoneNum=18366666666`

- 返回示例

```
{
    "status": "SUCCESS",
    "data": "优惠券分配成功"
}

```


### 13.2.2 web端查询优惠券接口

- 功能描述: 根据券号模糊匹配，类型，归属活动，状态查找符合条件的优惠券

- 请求地址: `http://domain/coupon/coupons/search`

- 请求动作: `GET`

- 请求示例: `http://localhost:8080/coupon/coupons/search?access_token=69ff3003-dee1-40d5-a36f-c0c4fa55c431&id=&type=1&activityId=5a13cc956c79211554a7f9ca&activityName=圣诞优惠&status=1&assignable=true&phoneNum=&page=0&size=2&sort =createdDate,DESC`

- 返回示例

```
sort=createdDate,DESC：按照优惠券生成时间降序排列

{
    "status": "SUCCESS",
    "data": {
        "content": [
            {
                "id": "5a273d7cde74ae16742721fd",
                "activityName": "活动7",
                "type": 1,
                "creator": null,
                "createDate": "2017-12-06 08:44:44",
                "validStartDate": "2017-11-21 19:30:30",
                "validEndDate": "2017-11-24 12:30:30",
                "status": 2,
                "phoneNum": "15555417041",
                "origin": 1,
                "assignable": true,
                "rule": {
                    "type": 1,
                    "freeHours": 2,
                    "generateNum": 2,
                    "maxNum": 2
                },
                "roadSections": [
                    {
                        "id": 1001,
                        "name": "植保路"
                    },
                    {
                        "id": 1002,
                        "name": "长江路"
                    }
                ],
                "receiveTime": null,
                "usedTime": null,
                "orderId": null
            },
            {
                "id": "5a273d7cde74ae16742721fe",
                "activityName": "活动7",
                "type": 1,
                "creator": null,
                "createDate": "2017-12-06 08:44:44",
                "validStartDate": "2017-11-21 19:30:30",
                "validEndDate": "2017-11-24 12:30:30",
                "status": 2,
                "phoneNum": "15555417041",
                "origin": 1,
                "assignable": true,
                "rule": {
                    "type": 1,
                    "freeHours": 2,
                    "generateNum": 2,
                    "maxNum": 2
                },
                "roadSections": [
                    {
                        "id": 1001,
                        "name": "植保路"
                    },
                    {
                        "id": 1002,
                        "name": "长江路"
                    }
                ],
                "receiveTime": null,
                "usedTime": null,
                "orderId": null
            },
            {
                "id": "5a273d7cde74ae16742721ff",
                "activityName": "活动7",
                "type": 3,
                "creator": null,
                "createDate": "2017-12-06 08:44:44",
                "validStartDate": "2017-11-21 10:30:30",
                "validEndDate": "2017-11-24 10:30:30",
                "status": 2,
                "phoneNum": "18365265123",
                "origin": 1,
                "assignable": true,
                "rule": {
                    "type": 3,
                    "useLimitAmount": 5,
                    "discountAmount": 2,
                    "generateNum": 2,
                    "maxNum": 2
                },
                "roadSections": [
                    {
                        "id": 1001,
                        "name": "植保路"
                    },
                    {
                        "id": 1002,
                        "name": "长江路"
                    }
                ],
                "receiveTime": null,
                "usedTime": null,
                "orderId": null
            },
            {
                "id": "5a273d7cde74ae1674272200",
                "activityName": "活动7",
                "type": 3,
                "creator": null,
                "createDate": "2017-12-06 08:44:44",
                "validStartDate": "2017-11-21 10:30:30",
                "validEndDate": "2017-11-24 10:30:30",
                "status": 2,
                "phoneNum": "18365265123",
                "origin": 1,
                "assignable": true,
                "rule": {
                    "type": 3,
                    "useLimitAmount": 5,
                    "discountAmount": 2,
                    "generateNum": 2,
                    "maxNum": 2
                },
                "roadSections": [
                    {
                        "id": 1001,
                        "name": "植保路"
                    },
                    {
                        "id": 1002,
                        "name": "长江路"
                    }
                ],
                "receiveTime": null,
                "usedTime": null,
                "orderId": null
            },
            {
                "id": "5a273d7cde74ae1674272201",
                "activityName": "活动7",
                "type": 3,
                "creator": null,
                "createDate": "2017-12-06 08:44:44",
                "validStartDate": "2017-11-21 10:30:30",
                "validEndDate": "2017-11-24 10:30:30",
                "status": 1,
                "phoneNum": null,
                "origin": null,
                "assignable": true,
                "rule": {
                    "type": 3,
                    "useLimitAmount": 10,
                    "discountAmount": 5,
                    "generateNum": 2,
                    "maxNum": 2
                },
                "roadSections": [
                    {
                        "id": 1001,
                        "name": "植保路"
                    },
                    {
                        "id": 1002,
                        "name": "长江路"
                    }
                ],
                "receiveTime": null,
                "usedTime": null,
                "orderId": null
            },
            {
                "id": "5a273d7cde74ae1674272202",
                "activityName": "活动7",
                "type": 3,
                "creator": null,
                "createDate": "2017-12-06 08:44:44",
                "validStartDate": "2017-11-21 10:30:30",
                "validEndDate": "2017-11-24 10:30:30",
                "status": 1,
                "phoneNum": null,
                "origin": null,
                "assignable": true,
                "rule": {
                    "type": 3,
                    "useLimitAmount": 10,
                    "discountAmount": 5,
                    "generateNum": 2,
                    "maxNum": 2
                },
                "roadSections": [
                    {
                        "id": 1001,
                        "name": "植保路"
                    },
                    {
                        "id": 1002,
                        "name": "长江路"
                    }
                ],
                "receiveTime": null,
                "usedTime": null,
                "orderId": null
            },
            {
                "id": "5a273d7cde74ae1674272203",
                "activityName": "活动7",
                "type": 2,
                "creator": null,
                "createDate": "2017-12-06 08:44:44",
                "validStartDate": "2017-11-21 10:30:30",
                "validEndDate": "2017-11-24 10:30:30",
                "status": 1,
                "phoneNum": null,
                "origin": null,
                "assignable": true,
                "rule": {
                    "type": 2,
                    "useLimitHour": 1,
                    "payAmount": 1,
                    "generateNum": 2,
                    "maxNum": 2
                },
                "roadSections": [
                    {
                        "id": 1001,
                        "name": "植保路"
                    },
                    {
                        "id": 1002,
                        "name": "长江路"
                    }
                ],
                "receiveTime": null,
                "usedTime": null,
                "orderId": null
            },
            {
                "id": "5a273d7cde74ae1674272204",
                "activityName": "活动7",
                "type": 2,
                "creator": null,
                "createDate": "2017-12-06 08:44:44",
                "validStartDate": "2017-11-21 10:30:30",
                "validEndDate": "2017-11-24 10:30:30",
                "status": 1,
                "phoneNum": null,
                "origin": null,
                "assignable": true,
                "rule": {
                    "type": 2,
                    "useLimitHour": 1,
                    "payAmount": 1,
                    "generateNum": 2,
                    "maxNum": 2
                },
                "roadSections": [
                    {
                        "id": 1001,
                        "name": "植保路"
                    },
                    {
                        "id": 1002,
                        "name": "长江路"
                    }
                ],
                "receiveTime": null,
                "usedTime": null,
                "orderId": null
            },
            {
                "id": "5a273d7cde74ae1674272205",
                "activityName": "活动7",
                "type": 2,
                "creator": null,
                "createDate": "2017-12-06 08:44:44",
                "validStartDate": "2017-11-21 10:30:30",
                "validEndDate": "2017-11-24 10:30:30",
                "status": 1,
                "phoneNum": null,
                "origin": null,
                "assignable": true,
                "rule": {
                    "type": 2,
                    "useLimitHour": 2,
                    "payAmount": 5,
                    "generateNum": 2,
                    "maxNum": 2
                },
                "roadSections": [
                    {
                        "id": 1001,
                        "name": "植保路"
                    },
                    {
                        "id": 1002,
                        "name": "长江路"
                    }
                ],
                "receiveTime": null,
                "usedTime": null,
                "orderId": null
            },
            {
                "id": "5a273d7cde74ae1674272206",
                "activityName": "活动7",
                "type": 2,
                "creator": null,
                "createDate": "2017-12-06 08:44:44",
                "validStartDate": "2017-11-21 10:30:30",
                "validEndDate": "2017-11-24 10:30:30",
                "status": 1,
                "phoneNum": null,
                "origin": null,
                "assignable": true,
                "rule": {
                    "type": 2,
                    "useLimitHour": 2,
                    "payAmount": 5,
                    "generateNum": 2,
                    "maxNum": 2
                },
                "roadSections": [
                    {
                        "id": 1001,
                        "name": "植保路"
                    },
                    {
                        "id": 1002,
                        "name": "长江路"
                    }
                ],
                "receiveTime": null,
                "usedTime": null,
                "orderId": null
            },
            {
                "id": "5a273d7cde74ae1674272207",
                "activityName": "活动7",
                "type": 4,
                "creator": null,
                "createDate": "2017-12-06 08:44:44",
                "validStartDate": "2017-11-21 10:30:30",
                "validEndDate": "2017-11-24 10:30:30",
                "status": 1,
                "phoneNum": null,
                "origin": null,
                "assignable": true,
                "rule": {
                    "type": 4,
                    "discountAmount": 5,
                    "generateNum": 2,
                    "maxNum": 1
                },
                "roadSections": [
                    {
                        "id": 1001,
                        "name": "植保路"
                    },
                    {
                        "id": 1002,
                        "name": "长江路"
                    }
                ],
                "receiveTime": null,
                "usedTime": null,
                "orderId": null
            },
            {
                "id": "5a273d7cde74ae1674272208",
                "activityName": "活动7",
                "type": 4,
                "creator": null,
                "createDate": "2017-12-06 08:44:44",
                "validStartDate": "2017-11-21 10:30:30",
                "validEndDate": "2017-11-24 10:30:30",
                "status": 1,
                "phoneNum": null,
                "origin": null,
                "assignable": true,
                "rule": {
                    "type": 4,
                    "discountAmount": 5,
                    "generateNum": 2,
                    "maxNum": 1
                },
                "roadSections": [
                    {
                        "id": 1001,
                        "name": "植保路"
                    },
                    {
                        "id": 1002,
                        "name": "长江路"
                    }
                ],
                "receiveTime": null,
                "usedTime": null,
                "orderId": null
            },
            {
                "id": "5a273d7cde74ae1674272209",
                "activityName": "活动7",
                "type": 4,
                "creator": null,
                "createDate": "2017-12-06 08:44:44",
                "validStartDate": "2017-11-21 10:30:30",
                "validEndDate": "2017-11-24 10:30:30",
                "status": 1,
                "phoneNum": null,
                "origin": null,
                "assignable": true,
                "rule": {
                    "type": 4,
                    "discountAmount": 10,
                    "generateNum": 2,
                    "maxNum": 2
                },
                "roadSections": [
                    {
                        "id": 1001,
                        "name": "植保路"
                    },
                    {
                        "id": 1002,
                        "name": "长江路"
                    }
                ],
                "receiveTime": null,
                "usedTime": null,
                "orderId": null
            },
            {
                "id": "5a273d7cde74ae167427220a",
                "activityName": "活动7",
                "type": 4,
                "creator": null,
                "createDate": "2017-12-06 08:44:44",
                "validStartDate": "2017-11-21 10:30:30",
                "validEndDate": "2017-11-24 10:30:30",
                "status": 1,
                "phoneNum": null,
                "origin": null,
                "assignable": true,
                "rule": {
                    "type": 4,
                    "discountAmount": 10,
                    "generateNum": 2,
                    "maxNum": 2
                },
                "roadSections": [
                    {
                        "id": 1001,
                        "name": "植保路"
                    },
                    {
                        "id": 1002,
                        "name": "长江路"
                    }
                ],
                "receiveTime": null,
                "usedTime": null,
                "orderId": null
            }
        ],
        "last": true,
        "totalElements": 14,
        "totalPages": 1,
        "size": 20,
        "number": 0,
        "first": true,
        "sort": null,
        "numberOfElements": 14
    }
}
```
### 13.2.3 web端根据券号查询优惠券信息

- 功能描述: 查询优惠券信息

- 请求地址: `http://domain/coupon/coupons/`

- 请求动作: `PUT`

- 请求示例: `localhost:8080/coupon/coupons/01ed9eac-1517-4782-9c89-d4dcd59bc14a?access_token=69ff3003-dee1-40d5-a36f-c0c4fa55c431`

- 返回示例
```
{
    "status": "SUCCESS",
    "data": {
        "id": "01ed9eac-1517-4782-9c89-d4dcd59bc14a",
        "activityName": "圣诞优惠",
        "type": 1,
        "creator": null,
        "createDate": "2017-11-30 12:00:36",
        "validStartDate": "2017-11-21 19:30:30",
        "validEndDate": "2017-11-28 12:30:30",
        "status": 2,
        "phoneNum": "15555417041",
        "origin": null,
        "assignable": true
    }
}

```

## 13.3 APP端优惠券访问接口


### 13.3.1 app用户领取优惠券接口

- 功能描述: 领取优惠券

- 请求地址: `http://domain/coupon/coupons/acquire`

- 请求动作: `PUT`

- 请求示例: `http://localhost:8080/coupon/coupons/acquire?access_token=10371f15-09c6-48de-9770-71603781a7f8`

- 请求示例

```
领取满减券：

{
	"activity":{
	"id":"5a13cc956c79211554a7f9ca",
	 "name":"圣诞优惠"
	},
	"rule": {
    "type":"3",
    "useLimitAmount":5,
    "discountAmount":2,
    "maxNum":2,
    "generateNum":5
   },
   "phoneNum":"18365265123",
   "origin":1
}

领取免费券：
{
	"activity":{
	"id":"5a1e1543e8452f12ec522c73",
	 "name":"停车活动"
	},
	"rule":{
    "type": "1",
    "freeHours": 2,
    "generateNum": 10,
    "maxNum": 2
  },
   "phoneNum":"18365265125",
   "origin":1
}

领取小时券：
{
	"activity":{
	"id":"5a1e1543e8452f12ec522c73",
	 "name":"停车活动"
	},
	"rule":{
     "type": "2",
     "useLimitHour": 1,
     "payAmount": 1,
     "generateNum": 10,
     "maxNum": 2
  },
   "phoneNum":"18365265126",
   "origin":1
}

领取直减券：
{
	"activity":{
	"id":"5a1e1543e8452f12ec522c73",
	 "name":"停车活动"
	},
	"rule": {
     "type": "4",
     "discountAmount": 5,
     "generateNum": 10,
     "maxNum": 1
  },
   "phoneNum":"18365265128",
   "origin":1
}
```
- 返回示例:
```
{
    "status": "SUCCESS"
}
```


### 13.3.2 app用户查看已领取的优惠券接口

- 功能描述: app用户查看优惠券

- 请求地址: `http://domain/customer/coupons/search`

- 请求动作: `GET`

- 请求示例: `http://localhost:8080/customer/coupons/search?access_token=eff26f7a-a1cf-46ae-8d17-a61b1c7ed87c&status=2&page=1&size=2&sort=type,DESC`

- 返回示例

```
status=2 未使用的优惠券：
status=3:已使用的优惠券：
status=4:已失效的优惠券：

sort=type,DESC 按照优惠券类型降序排序

{
    "status": "SUCCESS",
    "data": {
        "content": [
            {
                "id": "5a694f5f3536bc1d10ade964",
                "activityName": "测试活动",
                "template": {
                    "validStartDate": "2017-11-21 19:30:30",
                    "validEndDate": "2018-11-24 12:30:30",
                    "roadSections": [
                        {
                            "id": 1001,
                            "name": "植保路"
                        },
                        {
                            "id": 1002,
                            "name": "长江路"
                        }
                    ],
                    "isWholeRoadSection": false
                },
                "rule": {
                    "type": 1,
                    "freeHours": 2,
                    "generateNum": 2,
                    "maxNum": 2
                },
                "status": 1
            }
        ],
        "pageable": {
            "sort": {
                "sorted": false,
                "unsorted": true
            },
            "offset": 0,
            "pageSize": 20,
            "pageNumber": 0,
            "unpaged": false,
            "paged": true
        },
        "totalElements": 1,
        "last": true,
        "totalPages": 1,
        "size": 20,
        "number": 0,
        "sort": {
            "sorted": false,
            "unsorted": true
        },
        "numberOfElements": 1,
        "first": true
    }
}
```



### 13.3.3 app用户驶离结算时查看优惠券接口

- 功能描述: app用户驶离时根据路段查询当前可用的优惠券列表

- 请求地址: `http://domain/customer/coupons/obtainAvailableCoupons`

- 请求动作: `GET`

- 请求参数:
   - `roadSectionId`: 路段id
   - `roadSectionName`: 路段名称
   - `chargingStrategyId`: 收费策略id
   - `startTime`: 驶入时间
   - `vehicleType`: 车辆类型
   
- 请求示例: `http://localhost:8080/customer/coupons/obtainAvailableCoupons?access_token=a52d6375-7618-48f6-8267-d94b59966390&roadSectionId=1003&roadSectionName=1003路段&chargingStrategyId=1000&startTime=2017-11-28 7:00:00&vehicleType=02`

- 返回示例

```
   {
    "status": "SUCCESS",
    "data": [
        {
            "id": "2756299b-2881-4a79-875a-da591b7c196e",
            "rule": {
                "type": 4,
                "discountAmount": 1000,
                "generateNum": 5,
                "maxNum": 2
            },
            "template": {
                "validStartDate": 1511231430000,
                "validEndDate": 1511490630000,
                "roadSections": [
                    {
                        "id": 1003,
                        "name": "1003路段"
                    },
                    {
                        "id": 1002,
                        "name": "1002路段"
                    }
                ],
                "isWholeRoadSection": false
            }
        }
    ]
}
```

### 13.3.4 查询当前最新优惠活动

- 功能描述: 查询当前最新优惠活动

- 请求地址: `http://domain/coupon/activities/latest`

- 请求动作: `GET`

- 请求参数：
    - `platform`: 活动所属平台, APP活动为1
    
- 请求示例: `localhost:8080/coupon/activities/latest?access_token=7df15a7c-6187-4a7d-9ad4-9db597fadf6f&platform=1`

- 返回示例

```
   {
    "status": "SUCCESS",
    "data": {
        "id": "5a1fd3abdcd5d30a33b13256",
        "name": "中秋优惠",
        "rules": [
            {
                "type": 1,
                "freeHours": 2,
                "generateNum": null,
                "maxNum": 2
            }
        ]
    }
}
```


## 13.4 APP端优惠券结算访问接口

### 13.4.1 app自主驶出结算订单时，计算使用优惠券后的订单金额

- 功能描述: 计算优惠券金额

- 请求地址: `http://domain/billing/chargingStrategies/couponFee`

- 请求动作: `PUT`

- 请求参数(Request Parameter):
    - `chargingStrategyId`: 策略id
    - `startTime`: 订单开始时间
    - `vehicleType`: 车辆类型
    
- 请求示例: `http://http://localhost:8080/billing/chargingStrategies/couponFee?access_token=69ff3003-dee1-40d5-a36f-c0c4fa55c431&chargingStrategyId=1000&startTime=2017-11-28 7:00:00&vehicleType=02`

- 请求示例(Request Body):
    - 免费券:
    
    ```json
        {
         "type":"1",
          "freeHours": 2
        }
    ```
    - 小时券:
    
    ```json
    {
     "type":"2",
      "useLimitHour": 2,
      "payAmount": 5000
    }
    ```
    - 满减券:
    
    ```json
    {
     "type":"3",
     "useLimitAmount":5000,
      "discountAmount":2000
    }
    ```
    - 直减券:
    
    ```json
    {
      "type": "4",
      "discountAmount": 5
    }
    ```
- 返回参数:
    - `fee`: 优惠后的金额,分
    - `calculatedFee`: 计费金额(未使用优惠券时的金额),分
    - `endTime`: 计费截止时间
    - `parkingPeriod`: 停车时长,分钟
- 返回示例:

```json
{
    "status": "SUCCESS",
    "data": {
        "fee": 17800,
        "calculatedFee": 18700,
        "endTime": "2017-12-01 11:45:19.197",
        "parkingPeriod": 2775
    }
}
```    
         
         


