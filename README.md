# Sudoku
通过输入数独矩阵可以返回候选值或答案

***程序已编译为exe文件，可下载使用***

## code:
```python
from numpy import array
from numpy import zeros
import time
print("本程序为数独辅助工具\n请按行输入数独表格内容,未知数请填0，用空格分隔，输入完一行按回车\n--------------------------------------------------------------------------------\n")
row1=input("请输入第1行：")
row2=input("请输入第2行：")
row3=input("请输入第3行：")
row4=input("请输入第4行：")
row5=input("请输入第5行：")
row6=input("请输入第6行：")
row7=input("请输入第7行：")
row8=input("请输入第8行：")
row9=input("请输入第9行：")
data=row1+' '+row2+' '+row3+' '+row4+' '+row5+' '+row6+' '+row7+' '+row8+' '+row9

def uudu(data,flag):
    if flag==1:    
        data=array(data.split(),dtype=int).reshape((9,9))
        dict_data={}
        for i in range(9):
            for j in range(9):
                if data[i,j]==0:
                    dict_data[str(i)+str(j)]=set(range(10))-set(data[i,:])-set(data[:,j])
        
        keys = dict_data.keys()
        
        for i in keys:
            r=int(i[0])+1
            n=int(i[1])+1
            print('第',r,'行',n,'列的候选值为：' )
            #print("第%q行%p列的候选值为：" %(q,p))
            print(dict_data[i])
    
    elif flag==2:    
        print('the solution :')
        data=array(data.split(),dtype=int).reshape((9,9))
        
        def nine(data): #将数据划分成3*3的矩阵
            nine_data=zeros((3,3,3,3))
            for i in range(3):
                for j in range(3):
                    nine_data[i,j]=data[i*3:(i*3)+3,j*3:(j*3)+3]
            return nine_data
        
        def fill_value(data,nine_data): #输出每个空格中能够填的数字
            dict_data={} #建立一个空字典
            for i in range(9):
                for j in range(9):
                    if data[i,j]==0:
                        dict_data[str(i)+str(j)]=set(range(10))-set(data[i,:])-set(data[:,j])\
                        -set(nine_data[i//3,j//3].flatten()) #通过减法找出每个空格可选填的数字
            dict_data=sorted(dict_data.items(),key=lambda x:len(x[1])) #输出结果按照可选填数字个数升序排序
            return dict_data
        
        def insert_data(data):
            start_time=time.time() #开始时间
            insert_data=[] #建立空字典用来记录插入顺序
            while True:
                dict_data=fill_value(data,nine(data)) #生成每个空格中能够填的数字
                if len(dict_data) == 0: break #如果可选填的空格为0（表示所有空格以全部填完），则跳出while循环
                fisrt_values=dict_data[0] #取候选字典中第一个值（已排序）        
                key=fisrt_values[0]
                value=list(fisrt_values[1])
                insert_data.append((key,value)) #记录插入位置和插入值
                if len(value)!=0: #判断插入值是否为空
                    data[int(key[0]),int(key[1])]=value[0]
                else: #（如果插入值为空，则说明在前面某一步选值出现问题，需要回溯）
                    insert_data.pop() #将插入值为空的位置和值从记录字典中删除
                    for i in range(len(insert_data)): #此循环的目的是往上回溯i步，不一定需要回溯len(insert_data)步
                        recall=insert_data.pop() #取出出错位置的上一步
                        if len(recall[1])==1: #如果出错位置的上一步可选值为1，说明可能出错的地方还在前面
                            data[int(recall[0][0]),int(recall[0][1])]=0 #将出错位置的上一步处的值置为0
                        else:
                            data[int(recall[0][0]),int(recall[0][1])]=recall[1][1] #否则找到当初可能出错位置，在该位置处填入下一个候选值
                            insert_data.append((recall[0],recall[1][1:])) #重新记录填入位置和候选值
                            break #此处跳出的是上面的for循环，并非while循环
            end_time=time.time() #结束时间
            return data,end_time-start_time
    
        solution=insert_data(data)[0]
        for i in range(0,9):
            r=i+1
            print('the value of the row %r :' %r)
            print(solution[i])   
    
    else:
        print('erro opertation!')
    

flag=int(input('--------------------------------\n请输入1查看候选数，输入2查看结果: '))   
hjuu(data,flag)
gg=int(input('你可以输入2查看结果，否则任意键退出：'))
if gg==2:
    flag=2
    uudu(data,flag)
       
print("everything for Miss W.\r如有其它需求可联系开发者")
input("Input GOOD to end ：")
```

