# 关于`th:text`的测试
```java
	@RequestMapping("/success")
	public String success(Map<Object, Object> map) {
		map.put("hello", "<h1>你好</h1>");
		map.put("users", Arrays.asList("张三","<h2>王五</h2>","lierg"));
		return "dashboard";
	}
```

