setwd("c:/r_workdata")
getwd()
library(lubridate)
#2-2. 행렬로
sales2 = matrix(c(1,'Apple',500,5,
                  2,'Banana',200,2,
                  3,'Peach',100,4,
                  4,'Grape',50,7),4, by=T)
sales2
d1=data.frame(sales2)
d1

names(d1)=c('NO','NAME','PRICE','QTY')
d1

#데이터 조회
sales
sales$NO
sales[1,3]
sales[,2]

#원하는 조건만 검색 : subset()

subset(sales, qty <=5)
subset(sales, price==200)
subset(sales,name=='Apple')

#데이터 추가/합치기 : rbind(), cbind(), merge()
no=c(1,2,3)
name=c('apple','banana','peach')
price=c(100,200,300)
df1=data.frame(NO=no, NAME=name, PRICE=price)
df1

no=c(10,20,30)
name=c('train', 'car','ship')
price=c(1000,2000,3000)
df2=data.frame(NO=no, NAME=name, PRICE=price)

df1
df2

df3=cbind(df1,df2)
df4=rbind(df1,df2)
df4

df5=data.frame(name=c('apple','banana','cherry'), price=c(300,200,100))
df6=data.frame(name=c('apple','cherry','berry'), qty=c(10,20,30))
cbind(df5,df6)
rbind(df5,df6)

merge(df5,df6) #같은 값끼리만 합쳐짐. (apple, cherry)
merge(df5,df6,all = T)

#번호가 4,5이고, 이름이 'mango','berry' 와 가격이 각 400,500인 데이터 생성 후 df1행 추가
df1
n1=data.frame(NO=c(4,5),NAME=c('mango','berry'),PRICE=c(400,500))
df1=rbind(df1,n1)
df1

#수량이 (10,20,30,40,50)인 데이터를 열추가 하시오
df1=rbind(df1, qty=c(10,20,30,40,50))
df1

class(df1)
str(df1)

#데이터프레임에서 특정 컬럼만 골라내서 새로운 형태 만들기
no=c(1,2,3,4,5)
name=c('이순신','김유신','유관순','강감찬','안중근')
addr=c('서울','대전','대구','부산','광주')
tel=c(111,222,333,444,555)
hobby=c('놀','먹','자','게','멍')
mem=data.frame(NO=no, NAME=name, ADDR=addr, TEL=tel, HOBBY=hobby)
mem

mem2=subset(mem,select = c(NO,NAME,TEL))
mem2

mem3=subset(mem,select=-TEL)
mem3

colnames(mem3)=c('번호','이름','주소','취미')
mem3

mem
ncol(mem)
nrow(mem)
colnames(mem)
names(mem)
rownames(mem)
row.names(mem)

pro=c('사과','딸기','수박')
price=c(1803,1501,3040)
sell=c(24,38,13)
fru=data.frame(PRO=pro, PRICE=price, SELL=sell)
fru
colnames(fru)=c('제품','가격','판매량')

mean(fru$가격) #평균 내기
mean(fru$판매량)
round(mean(fru$가격),2) #소수점 끊기

colMeans(fru[,c('가격','판매량')])
colSums(fru[,c('가격','판매량')])/3

#데이터 수정: 변수명 바꾸기
install.packages("dplyr")
library(dplyr)

df1=data.frame(var1=c(1,2,1),
               var2=c(2,2,3))
df2 = df1

df2=rename(df2, v2=var2)
df2

#변수 조합해서 파생변수 만들기
df1

df1$var_sum=df1$var1+df1$var2
df1


install.packages("ggplot2")
library(ggplot2)

mpg
View(mpg)

class(mpg)
str(mpg)  #정수와 실수: num, 정수만: int
head(mpg) #처음부터 6개
tail(mpg) #끝에서 6개

mpg1=mpg
mpg1=rename(mpg1, city=cty)
mpg1=rename(mpg1, highway=hwy)
View(mpg1)

setwd("c:/r_workdata")

#작업용 데이터 읽기, 쓰기
#파일 이름 확인
list.files()
list.files(recursive = T) #폴더 안쪽까지 확인해준다

list.files(all.files = T) #숨김파일도 읽어옴

s1=scan("scan_1.txt") #텍스트 파일을 읽어서 벡터에 저장
s1
s1[3]

s2=scan("scan_2.txt",what="") #what: 읽어오는 값 형식 치환, 기본적으로는 정수 형태로 가져옴
s2

s3=scan("scan_3.txt",what="")
s3

s4=scan("scan_4.txt",what="")
s4

input = scan()
input

input2=scan(what="")
input2

input=scan()
input

input3=readline()  #한줄 읽기
input3

input4=readline("R U OK?")
input4


input5=readLines("scan_4.txt") #readLines() : 파일을 읽어서 벡터에 저장
input5

#read.table() : 데이터를 읽어서 데이터프레임에 저장
# - 주석이나 공백을 제외하고 읽는다.
#기본적으로 컬럼명이 없다고 판단
f=read.table("fruits.txt")
f

f2=read.table("fruits.txt", header=T) #컬럼명이 있다면 있다고 알려주기
f2

f2=read.table("fruits_2.txt")
f2

f2=read.table("fruits_2.txt", skip=2) #skip에는 주석이 포함되어 생략된다.
f2

f2=read.table("fruits_2.txt",nrows = 2) #nrow는 두줄만 출력한다.공백무시.
f2

f2=read.table("fruits_2.txt",skip=2,nrows = 2)
f2

#read.csv(): csv파일 읽기
#csv란 쉼표로 데이터를 나열해놓은 형식
#read.table()과 달리 컬럼명을 있다고 판단한다.

f3=read.csv("fruits_3.csv")
f3

f4=read.csv("fruits_4.csv")
f4

f4=read.csv("fruits_4.csv", header=F) #컬럼명이 없으니 만들어줘
f4

lab=c('NO','NAME','PRICE','QTY')
f4=read.csv("fruits_4.csv",header=F,col.names=lab) #컬럼명 만들어주면서 이름도 정해주기
f4

#read.csv()-> write.csv()
t3=read.csv("csv_test.txt")
t3
write(t3,"csv_3.csv")
write.table(t3,"csv_3.csv")
t4=read.csv("csv_3.csv")
t4

#read.table()->write.table()
#readLines()->write()
#
#readLines()/ read.table()/read.csv()
t1=read.csv("csv_test.txt")
t1

t2=readLines("csv_test.txt")
t2

t3=read.table("csv_test.txt")
t3

t3=read.table("csv_test.txt",sep=",") #구분자가 쉼표로 되어있다.
t3

t3=read.table("csv_test.txt",sep="," , header = T)
t3
