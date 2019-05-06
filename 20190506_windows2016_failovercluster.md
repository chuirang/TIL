# windows 2016 failover cluster 구성



## 절차

1. ad1 > DC 설치 > 새 포레스트로 설치
2. ac2 > DC 설치 > 기존 도메인에 DC 추가로 설치
3. sqla > AD Join 
4. sqls > AD Join
5. sqla, sqls > Failover Cluster 구성
6. sqla, sqls > SQL Server 설치



## 기본 환경

virtualbox 를 통하여 아래와 같은 vm을 생성하고 IP 계획 세움

| hostname                          | ip            |
| --------------------------------- | ------------- |
| ad1                               | 192.168.56.51 |
| ad2                               | 192.168.56.52 |
| sqla                              | 192.168.56.53 |
| sqls                              | 192.168.56.54 |
| failover cluster core resource IP | 192.168.56.61 |
| sql server service IP             | 192.168.56.62 |
| iscsi                             | 192.168.56.55 |
| Domain                            | w2016ad.com   |

![1557151539156](C:\Users\montauk\AppData\Roaming\Typora\typora-user-images\1557151539156.png)



#### virtualbox 를 통해 ad2 서버 DC 설치 간 발생한 에러

**※주의** : sysprep을 실행하면 설정한 내용이 날아가므로, 반드시 최초 세팅 시에 수행할 것!



virtualbox를 통하여 서버 설치 후 복제를 통하여 나머지 서버를 설치하였더니, SID가 교유하지 않아서 에러가 발생하였다. > sysprep 수행 필요

![1557157049427](C:\Users\montauk\AppData\Roaming\Typora\typora-user-images\1557157049427.png)



explorere > C:\Windows\System32\Sysprep 를 통하여 sysprep 수행

![1557157499794](C:\Users\montauk\AppData\Roaming\Typora\typora-user-images\1557157499794.png)



## failover cluster 설치

