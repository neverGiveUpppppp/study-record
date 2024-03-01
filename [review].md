

### @EnableCaching     
스프링의 캐싱 추상화   
Spring Framework의 캐시 추상화 기능 활성화 기능    
→ Spring의 캐시 관련 어노테이션(@Cacheable, @CacheEvict 등)을 사용    
→ @EnableCaching 없어도 Ehcache 등 다른 lib나 툴을 이용해 캐쉬 사용가능    
but, 스프링의 캐싱 추상화와 연동하는 게 이점이 많음    
<br>

### 스프링, 외부API call 5 way

1.HttpURLConnection/URLConnection    
2.HttpClient    
3.RestTemplate    
4.WebClient    
5.OpenFeign    

정리    
순수 자바 기반 구현으로 공부하고 싶다면?       1.HttpURLConnection/URLConnection    
레거시 및 실무를 위해서는?                               3.RestTemplate    
비동기 포함 성능 및 미래를 위해서는?              4.WebClient    
MSA에 적합                                                        5.OpenFeign    

자료 출처
https://jie0025.tistory.com/531



