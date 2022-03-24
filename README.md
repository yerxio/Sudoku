# Sudoku
通过输入数独矩阵可以返回候选值或答案
##code:
```python
from numpy import array
print("本程序为计算数独候选值的程序\n请按行输入数独表格内容,未知数请填0，用空格分隔，输入完一行按回车\n--------------------------------------------------------------------------------\n")
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

data=array(data.split(),dtype=int).reshape((9,9))
dict_data={}
for i in range(9):
    for j in range(9):
        if data[i,j]==0:
            dict_data[str(i)+str(j)]=set(range(10))-set(data[i,:])-set(data[:,j])



# 将字典拆分为键和值的列表

keys = dict_data.keys()

for i in keys:
    r=int(i[0])+1
    n=int(i[1])+1
    print('第',r,'行',n,'列的候选值为：' )
    #print("第%q行%p列的候选值为：" %(q,p))
    print(dict_data[i])
print("everything for Miss W.\r如有其它需求可联系开发者")
input("Input GOOD to end ：")
```
