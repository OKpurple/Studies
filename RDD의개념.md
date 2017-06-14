기본 개념 잡기

RDD 는 여러 분산 노드에 걸쳐서 저장되는 변경이 불가능한 데이타(객체)의 집합으로 각각의 RDD는 여러개의 파티션으로 분리가 된다. (서로 다른 노드에서 분리되서 실행되는). 

쉽게 말해서 스파크 내에 저장된 데이타를 RDD라고 하고, 변경이 불가능하다. 변경을 하려면 새로운 데이타 셋을 생성해야 한다.

RDD의 생성은 외부로 부터 데이타를 로딩하거나 또는 코드에서 생성된 데이타를 저장함으로써 생성할 수 있다.

RDD에서는 딱 두 가지 오퍼레이션만 지원한다.
Transformation : 기존의 RDD 데이타를 변경하여 새로운 RDD 데이타를 생성해내는 것. 흔한 케이스는 filter와 같이 특정 데이타만 뽑아 내거나 map 함수 처럼, 데이타를 분산 배치 하는 것 등을 들 수 있다.
Action : RDD 값을 기반으로 무엇인가를 계산해서(computation) 결과를 (셋이 아닌) 생성해 내는것으로 가장 쉬운 예로는 count()와 같은 operation들을 들 수 있다.

RDD의 데이타 로딩 방식은 Lazy 로딩 컨셉을 사용하는데, 예를 들어 sc.textFile(“파일”)로 파일을 로딩하더라도 실제로 로딩이 되지 않는다. 파일이 로딩되서 메모리에 올라가는 시점은 action을 이용해서 개선할 당시만 올라간다.
아래 코드를 보자 아래 코드는 “README.md” 파일을 RDD로 로딩 한후에

pythonLines에 “Python”이라는 단어를 가지고 있는 라인만 추려서 새로운 RDD를 만들고,
그 다음 count() action을 이용하여, 그 줄 수 를 카운트 하는 예제이다.







그렇다면, 언제 실제 README.md 파일이 읽혀질까? 실제로 읽혀지는 시기는 README.md 파일을 sc.textFile로 오픈할 때가 아니라 .count() 라는 액션이 수행될 때 이다.
이유는 파일을 오픈할때 부터 RDD를 메모리에 올려놓게 되면 데이타가 클 경우, 전체가 메모리에 올라가야 하는데, 일반적으로 filter 등을 이용해서 데이타를 정재한 후에,  action을 수행하기 때문에, action을 수행할때, action수행시 필요한 부분만 (filter가 적용된 부분만) 메모리에 올리면 훨씬 작은 부분을 올릴 수 있기 때문에 수행시에 데이타를 로딩하게 된다. 그렇다면 로딩된 데이타는 언제 지워질까?
action을 수행한다음 바로 지워진다.

위에서 보면 lines.count()를 두번 수행하였는데, 이 실행시 마다 README.md 파일을 다시 읽어드린다. 만약에, 한번 읽어드린 RDD를 메모리에 상주하고 계속해서 재 사용하고 싶다면 RDD.persist()라는 메서드를 이용하면, RDD를 메모리에 상주 시킬 수 있다.

RDD 생성하기

앞에서도 언급했듯이, RDD를 생성하는 방법은 크게 두가지가 있다. 
외부로 부터 파일을 읽어서 로딩하거나 파일은 일반 파일을 읽거나 S3,HBase,HDFS,Cassandra 등에서 데이타를 읽어올 수 있다. 
파이썬 예제) lines = sc.textFile(“/path/filename.txt”)
또는 드라이버 프로그램내에서 생성된 collection을 parallelize() 라는 메서드를 이용해서 RDD 화 하는 방법이다. (자바 컬렉션등을 RDD로 생성)
자바 예제) JavaRDD<String> lines = sc.parallelize(Array.asList(“first”,”second”))

RDD Operations

1) Transformation (변환)

변환은 RDD를 필터링하거나 변환하여 새로운 RDD를 리턴하는 오퍼레이션이다.
다음 코드는 README.md 라는 파일을 읽어서 f 라는 RDD를 생성한후
f라는 RDD 에서 “Apache”라는 문자열을 가진 라인만을 모아서 t라는 RDD를 새롭게 생성한 후 화면으로 출력하는 예제이다.
f와 t는 전혀 다른  RDD로 RDD t는 filter에 의해서 새롭게 생성되었다.



<그림. 파이썬 예제>


변환 함수는 filter 뿐 아니라, map, group등 여러가지 함수들이 있으며, 자세한 함수 리스트는 https://spark.apache.org/docs/latest/programming-guide.html#transformations 를 참고하기 바란다.

2) Action (액션)

액션은 RDD를 가지고 계산을 해서 최종 결과를 리턴하거나 또는 데이타를 외부 저장소(External Storage)등에 쓸 수 있다.
최종 결과를 리턴하는 오퍼레이션으로는 앞의 예제에서도 설명한 count()나, 첫번째 element를 리턴하는 first등이 있으며, RDD를 저장하는 오퍼레이션으로는 saveAsTextFile(path)와 같은 오퍼레이션등이 있다.
 

https://spark.apache.org/docs/latest/programming-guide.html#actions

본 포스팅을 오라일사의 "Learning Spark" 과  Sparing Programming Guide를 참고하여 작성하였습니다. https://spark.apache.org/docs/latest/programming-guide.html


출처: http://bcho.tistory.com/1027 [조대협의 블로그]