### 03/17(월)
- Algorithm 90m.
	- 소수 판별 
		- 2부터 자기 자신이 나누어지는 지 확인.
		- (에라토스테네스의 체) Math.sqrt(n), n의 제곱근
	- BackTracking | DFS
		- **BackTracking**
			- 탐색 진행 시, 상태를 변경한 후, 다시 원래대로 돌리는 방식
```Java
for (int i = 0; i < numbers.length; i++) {
	if (!visited[i]) { // 방문하지 않은 경우만 진행
		visited[i] = true; // 선택 (상태 변경)
		dfs(numbers, path + numbers[i], visited); // 재귀 탐색
		visited[i] = false; // 백트래킹 (상태 복원)
	}
```
- Develop-Blog 90m.
- JobSearching 30m.