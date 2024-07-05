"""
在一个桌子的边缘不停的叠木板（从下边加木板），要求木板从桌沿延伸出去尽量长的距离
这样叠起来的一个模板塔可以从桌沿延伸出多少距离？
答案是无穷，每次叠放木板，新的木板可以延伸出的距离是一个调和级数
编写程序验证
"""

for i in range(1,1000):
    for j in range(1,i):
        locals()['x'+str(j)+'_equ'] = locals()['x'+str(j)] - z
        locals()['y'+str(j)+'_equ'] = locals()['y'+str(j)] + z
    locals()['x'+str(i)+'_equ'] = 1 - z
    locals()['y'+str(i)+'_equ'] = z
    equation = 0
    for j in range(1,i+1):
        equation += locals()['x'+str(j)+'_equ']
        equation -= locals()['y'+str(j)+'_equ']
    locals()['z'+str(i)] = float(sympy.solve(equation, z)[0])
    for j in range(1,i):
        locals()['x'+str(j)] = locals()['x'+str(j)] - locals()['z'+str(i)]
        locals()['y'+str(j)] = locals()['y'+str(j)] + locals()['z'+str(i)]
    locals()['x'+str(i)] = 1 - locals()['z'+str(i)]
    locals()['y'+str(i)] = locals()['z'+str(i)]

sum0 = 0
for i in range(1,1000):
    number = locals()['z'+str(i)]
    sum0+=number
    number = Fraction(number).limit_denominator()
    print(number)
    
print(sum0)
