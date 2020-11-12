---
typora-root-url: ./img/20201112/스크린샷 2020-11-12 오후 4.22.23.png
---

# 01 @RequestParam, @RequestBody 알아보기

# 1. @RequestParam, @RequestBody 학습

1. @RequestParam이란?
2. @RequestBody란?



## 1.1 @RequestParam이란?

@RequestParam 어노테이션은 HttpServletRequest 객체와 같은 역할을 한다.



## 1.2 @RequestBody란?

@RequestBody 어노테이션은 Body형태로 객체를 가져와 입력한다.

```
@RestController
@RequestMapping(value = "/home/host")
@Slf4j
public class ItemController {
	
	@Autowired
	private ZabbixItemApi zabbixItemApi;
	
	/**
	 *
	 * METHOD : getItem
	 * DESCRIPTION : hostid를 전달하여 해당 호스트의 아이템 조회 컨트롤러 	
	 *
	 * @param request
	 * @return
	 *
	 */
	@PostMapping(value="/getItem")
	public Map<String, Object> getItem(@RequestBody ItemApiVO itemApiVO){ //다음과 같이 객체 형식으로 가져올 수 있음
		Map<String, Object> result = new HashMap<>();
		String hostid = itemApiVO.getHostid();
		System.out.println("request : "+hostid);
		result.put(ModelKeyCd.RESULT_CODE.getCode(), SuccessFailCd.SUCCESS.getCode());
		result.put(ModelKeyCd.RESULT_DATA.getCode(), zabbixItemApi.getItem(hostid));
		return result;
	}
```



postman으로 다음과 같이 입력시 body > raw > json 형태로 설정 후 입력하면 아래와 같은 response 값을 확인할 수 있다.

<img src='/img/20201112/20201112_img1.png'><br>

