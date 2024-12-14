1. Java의 Redis Client 종류
	- Jedis
		- 멀티스레드 환경에서 Jedis를 사용하는 방법은 연결 풀링을 사용하는 것입니다. 
		- Jedis를 사용하는 각 동시 스레드는 상호 작용 `Jedis`기간 동안 자체 인스턴스를 얻습니다. 
		- 연결 풀링은 인스턴스당 물리적 ​​연결의 비용으로 제공되며, 이는 Redis 연결 수를 증가시킵니다.
	- Lettuce
		- Lettuce는 netty 기반으로 구축되었으며 연결 인스턴스(`StatefulRedisConnection`)는 여러 스레드에서 공유될 수 있습니다. 
		- 따라서 멀티스레드 애플리케이션은 Lettuce와 상호 작용하는 동시 스레드 수에 관계없이 단일 연결을 사용할 수 있습니다.
