```
public static void main(String[] args)
{
	ByteBuffer buf = ByteBuffer.allocate(30);
	System.out.println("쓰기");
	log(buf);
	buf.put("1234".getBytes());
	log(buf);
	buf.put("5678".getBytes());
	log(buf);
	buf.clear();
	log(buf);
	buf.put("9012".getBytes());
	log(buf);
	buf.compact();
	log(buf);
	System.out.println("다시 쓰기");
	buf.clear();
	buf.put("3456".getBytes());
	log(buf);
	System.out.println("읽기 모드");
	buf.flip();
	log(buf);
	String msg = new String(buf.array(), buf.position(), buf.limit());
	System.out.println("마지막 메시지는 ["+msg+"]!!");
}
 
public static void log(ByteBuffer buf)
{
	System.out.println(buf.position() + " ~ " + buf.limit() + " [" + new String(buf.array()) + "]");
}
/** 출력값 [설명포함]
쓰기
0 ~ 30 [                              ] : 처음생성됨
4 ~ 30 [1234                          ] : buf.put("1234".getBytes());
8 ~ 30 [12345678                      ] : buf.put("5678".getBytes());
0 ~ 30 [12345678                      ] : buf.clear(); // 글자는 그대로! 정확히 포지션/리미트를 클리어 하는 겁니다. 
4 ~ 30 [90125678                      ] : buf.put("9012".getBytes()); // 포지션이 클리어 되었으니 0부터 다시 쓰기를 합니다.
26 ~ 30 [5678                          ] : buf.compact();
							// 그전 4 ~ 30 이선택된 상태! 그렇다면 현재 4~30까지가 선택된 상태가 됩니다.
							// 4 ~ 30을 앞당기면 0 ~ 26 이되며 다음 위치를 선택하기 때문에 26 ~ 30 이 됩니다.
다시 쓰기
4 ~ 30 [3456                          ] : buf.clear(); buf.put("3456".getBytes()); // 포인터 위치를 초기화 한 후 다시 글자를 씁니다.
읽기 모드
0 ~ 4 [3456                          ] : buf.flip(); 리미트를 마지막 포지션으로 포지션을 0으로 바꿈으로써 마지막으로 썼던 버퍼를 읽기 좋은 위치로 세팅합니다.
마지막 메시지는 [3456]!! : buf.flip(); 이 없었다면 마지막 메시지는 [                          ] 가 리드되었을겁니다.
*/

```



```
ByteBuffer buf = ByteBuffer.allocate(100);
System.out.println("처음생성");
System.out.println(buf.capacity());
System.out.println(buf.limit());
System.out.println(buf.position());
 
buf.flip();
System.out.println("flip!!");
System.out.println(buf.capacity());
System.out.println(buf.limit());
System.out.println(buf.position());
 
/** 출력값
처음생성
100
100
0
flip!!
100
0
0
*/
```



int capacity ()

- 전체 크기입니다. 처음 allocate / allocateDirect 에 할당된 크기를 반환합니다.
- 이 값은 객체가 소멸할때까지 변하지 않습니다.

int position()

- 포인터의 시작 포지션 입니다, 첫 생성값은 0 입니다.

int limit()

- 포인터의 끝, 첫 생생값은 capacity() 와 동일합니다.