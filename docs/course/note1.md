# 第一章 线性代数方程组的直接求解


```python
import copy
```

## 定义Matrix类


```python
class Matrix:
	def __init__(self, row, column, fill = 0.0):
		'''row为行数，column为列数，生成零矩阵'''
		self.shape = (row, column)
		self.row = row
		self.column = column
		self._matrix = [[fill]*column for i in range(row)]


	def __getitem__(self, index):
		'''如果index是一个数，则返回一行，如果是一个元组则返回对应的元素'''
		if isinstance(index, int):
			return self._matrix[index-1]
		elif isinstance(index, tuple):
			return self._matrix[index[0]-1][index[1]-1]


	def __setitem__(self, index, value):
		'''如果index 是一个数，则将对应行修改为value，这里使用了copy模块'''
		if isinstance(index, int):
			self._matrix[index-1] = copy.deepcopy(value)
		elif isinstance(index, tuple):
			self._matrix[index[0]-1][index[1]-1] = value
	

	def __eq__(self, N):
		'''比较自身与N，这里比较的是维度，可以改成别的'''
		assert isinstance(N, Matrix), "类型不匹配的对象不能比较"
		return N.shape == self.shape


	def __add__(self, N):
		'''加法'''
		assert N.shape == self.shape, "维度不同不能相加"
		M = Matrix(self.row, self.column)
		for r in range(self.row):
			for c in range(self.column):
				M[r, c] = self[r, c] + N[r, c]
		return M


	def __sub__(self, N):
		'''减法'''
		assert N.shape == self.shape, "维度不同不能相减"
		M = Matrix(self.row, self.column)
		for r in range(self.row):
			for c in range(self.column):
				M[r, c] = self[r, c] - N[r, c]
		return M

	
	def __mul__(self, N):
		'''乘法，分为数乘和矩阵乘法'''
		if isinstance(N, int) or isinstance(N, float):
			M = Matrix(self.row, self.column)
			for r in range(self.row):
				for c in range(self.column):
					M[r, c] = self[r, c] * N	
		else:
			assert N.row == self.column, "维度不匹配不能相乘"
			M = Matrix(self.row, self.column)
			for r in range(self.row):
				for c in range(N.column):
					sum = 0
					for k in range(self.column):
						sum += self[r, k] * N[k, c]
					M[r, c] = sum
		return M


	def __div__(self, N):
		'''矩阵没有除法'''
		pass


	def __pow__(self, k):
		'''乘方'''
		assert self.row == self.column, "不是方阵，不能乘方"
		M = copy.deepcopy(self)
		for i in range(k):
			M = M * self
		return M


	def rank(self):
		'''矩阵的秩'''
		pass


	def trace(self):
		'''矩阵的迹'''
		pass


	def adjoint(self):
		'''伴随矩阵'''
		pass


	def invert(self):
		'''逆矩阵'''
		assert self.row == self.column, "不是方阵"
		M = Matrix(self.row, self.column*2)
		I = self.identity()
		
		for r in range(1, M.row+1):
			temp = self[r]
			temp.extend(I[r])
			M[r] = copy.deepcopy(temp)
		
		for r in range(1, M.row+1):
			if M[r, r] == 0:
				for rr in range(1, M.row+1):
					if M[rr, r] != 0:
						M[r], M[rr] = M[rr], M[r]
					break
			
			assert M[r, r] != 0, "矩阵不可逆"

			temp = M[r, r]
			for c in range(r, M.column+1):
				M[r, c] /= temp

			for rr in range(1, M.row+1):
				temp = M[rr, r]
				for c in range(r, M.column+1):
					if rr == r:
						continue
					M[rr, c] -= temp * M[r, c]
		
		N = Matrix(self.row, self.column)
		for r in range(1, self.row+1):
			N[r] = M[r][self.row:]
		N.show()


	def transpose(self):
		'''转置'''
		M = Matrix(self.column, self.row)
		for c in range(self.column):
			for r in range(self.row):
				M[c, r] = self[r, c]
		return M


	def cofactor(self, row, column):
		'''方阵代数余子式'''
		assert self.row == self.column, "不是方阵，无法计算方阵代数余子式"
		assert self.row >= 3, "至少是3*3方阵"
		assert row <= self.row and column <= self.column, "下标超出范围"
		
		M = Matrix(self.row-1, self.column-1)
		for r in range(self.row):
			if r == row:
				continue
			for c in range(self.column):
				if c == column:
					continue
				rr = r-1 if r > row else r
				cc = c-1 if c > column else c
				M[rr, cc] = self[r, c]
		return M


	def det(self):
		'''计算行列式'''
		assert self.row == self.column, "不是方阵，无法计算行列式"
		if self.shape == (2, 2):
			return self[1, 1] * self[2, 2] - self[1, 2] * self[2, 1]
		else:
			sum = 0.0
			for c in range(self.column + 1):
				sum += (-1) ** (c + 1) * self[1, c] * self.cofactor(1, c).det()
			return sum


	def zeros(self):
		'''全零矩阵'''
		M = Matrix(self.row, self.column, fill = 0.0)
		return M


	def ones(self):
		'''全1矩阵'''
		M = Matrix(self.row, self.column, fill = 1.0)
		return M


	def identity(self):
		'''相同维度的单位矩阵'''
		assert self.row == self.column, "非c乘n矩阵没有单位矩阵"
		M = Matrix(self.row, self.column)
		for r in range(self.row):
			for c in range(self.column):
				if r == c:
					M[r, c] = 1.0
				else:
					M[r, c] = 0.0
		return M


	def show(self):
		'''打印矩阵'''
		for r in range(self.row):
			for c in range(self.column):
				print(self[r+1, c+1], end = " ")
			print()
```

## 下三角矩阵


```python
def lower_triangular(L, b):
	assert isinstance(L, Matrix), "L is not a Matrix"
	assert L.row == L.column, "L is not an upper triangular matrix"
	assert isinstance(b, Matrix), "b is not s Matrix"
	assert L.row == b.row, "L's row != b's row"

	n = L.row
	x = Matrix(n, 1)
	for i in range(1, n + 1):
		assert L[i, i] != 0, "i="+ str(i) +" ,lii=0, Unable to calculate"
		x[i] = b[i]	# deepcopy
		for j in range(1, i):
			x[i, 1] += -L[i, j] * x[j, 0]
		x[i, 0] = x[i, 0] / L[i, i]
	return x
```

## 上三角矩阵


```python
def upper_triangular(U, b):
	assert isinstance(U, Matrix), "U is not a Matrix"
	assert U.row == U.column, "U is not an upper triangular matrix"
	assert isinstance(b, Matrix), "b is not s Matrix"
	assert U.row == b.row, "U's row != b's row"

	n = U.row
	x = Matrix(n, 1)
	for i in range(n, 0, -1):
		assert U[i, i] != 0, "i="+ str(i) +" ,uii=0, Unable to calculate"	
		x[i] = b[i]	# deepcopy
		for j in range(n, i, -1):
			x[i, 1] += -U[i, j] * x[j, 0]
		x[i, 0] = x[i, 0] / U[i, i]
	return x
```

## 高斯消元


```python
def Gaussian_elimination(L, b):
	A = copy.deepcopy(L)
	assert isinstance(A, Matrix), "A is not a Matrix"
	assert A.row == A.column, "A is not an upper triangular matrix"
	assert isinstance(b, Matrix), "b is not s Matrix"
	assert A.row == b.row, "A's row != b's row"

	n = A.row
	for k in range(1, n):
		assert A[k, k] != 0, "k="+ str(k) +" ,akk=0, Unable to calculate"
		for i in range(k+1, n+1):
			c = - A[i, k] / A[k, k]
			for j in range(k+1, n+1):
				A[i, j] += c * A[k, j]
			b[i, 1] += c * b[k, 1]
	x = upper_triangular(A, b)

	return x
```

## LU分解
**如果A的各阶顺序主子式均不为零（即各顺序主子阵均非奇异），则如下两种分解是唯一的**

**杜利特尔分解**：单位下三角矩阵L，非奇异三角矩阵U

**克劳特分解**：单位上三角矩阵U，一般下三角矩阵L

### LU分解的用途

* 高效地求解多右端方程组的问题

$$A=LU,Ax=b$$

$$x=A^{-1}b=U^{-1}L^{-1}b$$

分解为两步：\(Ly=b\)和\(Ux=y\)，分别使用前代和回代过程

* 求解A的逆矩阵

* 计算矩阵的行列式

$$det(A)=det(L)det(U)=det(U)$$


```python
def L_U(A):
	assert isinstance(A, Matrix), "A is not a Matrix"
    
	n = A.row
	for k in range(1, n):
		assert A[k, k] != 0, "k="+ str(k) +" ,akk=0, Unable to calculate"
		
		for i in range(k+1, n+1):
			for j in range(1, k):
				A[i, k] += -A[j, k] * A[i, j]
			A[i, k] = A[i, k] / A[k, k]
		
		for j in range(k+1, n+1):
			for i in range(1, k+1):
				A[k+1, j] += -A[k+1, i] * A[i, j]
	return A
```

## 三角方程组的追赶法

$$Ax=f$$

使用三个向量a，b，c表示非零元素

$$a=(a_2,a_3,...,a_n)$$

$$a=(b_1,b_2,...,b_n)$$

$$a=(c_1,c_2,...,c_{n-1})$$

追赶法实施的条件

$$|b_1|>|c_1|>0$$

$$|b_k|\geq|a_k|+|c_k|>0$$

$$|b_n|>|a_n|>0$$

此时能满足所有的顺序主子式均非奇异



```python
def Tomas(a,b,c,f):
    # 此部分代码未完成
    '''a,b,c,f are all Matrixes'''
    assert isinstance(a, Matrix), "a isn't a Matrix"
    assert isinstance(b, Matrix), "b isn't a Matrix"
    assert isinstance(c, Matrix), "c isn't a Matrix"
    assert isinstance(f, Matrix), "f isn't a Matrix"

    n = b.column
    for i in range(2, n+1, 1):
        m = a[i, 1] / b[i-1, 1]
        b[i, 1] = b[i, 1] - m * c[i-1, 1]
        f[i, 1] = f[i, 1] - m * f[i-1, 1]
    x = Matrix(n, 1)
    for i in range(n-1, 0, -1):
        x[i, 1] = (f[i-1] - c[i, 1] * x[i+1, 1]) / b[i, 1]
```

## 列主元消去法

高斯消元法：按照自然顺序逐一进行的，顺利进行的条件是顺序主子式都不为零
高斯消去法可能出现的问题：

* \(a^{(k)}_{kk}=0\)使计算中断

* \(a^{(k)}_{kk}\neq0\)但是非常小，作除数使误差快速传播

解决办法：选主元消去法

* **部分主元/列主元消去法**：选取当前列里未消去部分的最大元素作为主元，交换那一行与当前行

* **全主元消去法**：在未消去的子矩阵中所有元素里选取最大的一个，通过行、列变化交换到当前对角元的位置，这一方法非常稳定，但计算量比列主元大很多

列主元消去法可以顺便算出行列式


```python
def Gaussian_elimination_Maximal_Column(L, b):
	A = copy.deepcopy(L)
	assert isinstance(A, Matrix), "A is not a Matrix"
	assert A.row == A.column, "A is not an upper triangular matrix"
	assert isinstance(b, Matrix), "b is not s Matrix"
	assert A.row == b.row, "A's row != b's row"
    
	det = 1
	n = A.row
	for k in range(1, n):
		a_list = [A[i, k] for i in range(k, n+1)]
		a_max = a_list[0]
		index = k
		for i in range(k, n+1):
			if a_list[i-k] > a_max:
				a_max = a_list[i-k]
				index = i
        
		assert A[k, k] != 0, "k="+ str(k) +" ,akk=0, Unable to calculate, det = 0"
		if index != k:
			A[k], A[index] = A[index], A[k]
			b[k], b[index] = b[index], b[k]        
		for i in range(k+1, n+1):
			c = - A[i, k] / A[k, k]
			for j in range(k+1, n+1):
				A[i, j] += c * A[k, j]
			b[i, 1] += c * b[k, 1]
		det = A[k, k] * det
	det = det * A[n, n]
        
	x = upper_triangular(A, b)  

	return x, det
```

**比例因子选取主元**：

* 在每个方程的系数里找最大元素\(s_i\)

* 对某个\(i\)，若\(s_1=0​\)，则没有唯一解；否则计算​\(max{\frac{a_{k_1}}{s_k}}​\)，并选取最大的那个方程，与当前的第一个方程交换

* 对剩下的n-1个方程做相同操作

**比例因子选主元与列主元的区别**：比较的对象不同，列主元比的是第一个非零系数，比例因子比的是那个分数


```python
q = Matrix(3, 3)
q[1] = [12, -3, 3]
q[2] = [-18, 3, -1]
q[3] = [1, 1, 1]

b = Matrix(3, 1)
b[1, 1] = 1
b[2, 1] = 2
b[3, 1] = 3

m, n = Gaussian_elimination_Maximal_Column(q, b)
m.show()
print(n)
```

    0.030303030303030276 
    1.3787878787878787 
    1.5909090909090908 
    66.0


## 高斯-约当（Gauss-Jordan）消元法
同时消去对角线两侧的元素

总运算次数\((n^3+n^2-n)​\)比高斯消元法​\((\frac{2}{3}n^3+\frac{3}{2}n^2-\frac{7}{6}n)​\)大很多

G-Jx消元法的主要作用是求解逆矩阵\(A^{-1}\)

## 列主元LU分解
LU分解时同样采取部分主元法

LU分解时有行的交换，因此分解的是PA

P是个正交矩阵，每行只要有一个为1的元素，通常使用一个长度为n的整型数组p表示

## 部分主元消去法进行LU分解的计算量和储存
与直接的LU分解相比，增加了\((n-1)​\)次求最大值的运算，以及若干次矩阵的行交换

与直接的LU分解相比，储存量只增加了一个长度为n的整形数组

利用部分主元的LU分解可以方便地求解线性方程组，一般不会出现算法的中断，同时有效减小误差，也适合多右端问题

## 全主元LU分解

$$PAQ=LU$$

理论上极为稳定，但是计算量非常大，实际应用主要使用列主元消去法求解一般矩阵的线性方程组，该方法已经足够稳定且误差可控

## 对称正定矩阵的Cholesky分解
对称矩阵
$$a_{ij}=a_{ji}$$

**定理**：若A为n阶对称矩阵，且其各阶顺序主子式不为零，则A可以唯一地分解为

$$A=L_0DL_0^{T}$$

\(L_0​\)为单位下三角矩阵，​\(D​\)为对角矩阵

* 若A是对称正定矩阵，则\(D​\)为对称正定矩阵

**对称正定矩阵的Cholesky分解**

* \(A=LL^{T}​\)，​\(L​\)是非奇异下三角阵，对角元素大于零，分解方式唯一
* \(A=R^{T}R​\)，\(R\)是非奇异上三角阵

**古尔维兹定理**：实对称矩阵正定的充要条件是它的各阶顺序主子式为正

在分解之后，方程变为

$$Ly=b$$

$$L^Tx=y$$


```python
def Cholesky(A):
	assert isinstance(A, Matrix), "A is not a Matrix"
	assert A.row == A.column, "A is not an hhhhhhhhhh matrix"

	n = A.row
	for j in range(1, n+1):
		for k in range(1, j):
			A[j, j] = A[j, j] - A[j, k] ** 2
		A[j, j] = A[j, j] ** 0.5

		for i in range(j+1, n+1):
			for k in range(1, j):
				A[i, j] = A[i, j] - A[i, k] * A[j, k]
			A[i, j] = A[i, j] / A[j, j]

	return A
```

## 平方根法的改进

$$A=LDL^T$$

L是单位下三角矩阵，此方法避免了开平方运算，但乘积计算量大了一倍，因此继续引入辅助变量

## 一般对称正定带状系数矩阵方程组的算法

n阶对称正定带状矩阵，带宽2m+1，可以稳定分解成\(A=LDL^T​\)，T为下半带宽为m的带状阵

# 向量和矩阵的范数（暂略）

# 线性方程组的性态

\(||A||\ ||A^{-1}||​\)刻画了方程组的“病态程度”

病态方程的经验判断：

* 使用主元消去时使用小主元

* A的最大特征值和最小特征值之比很大

* 有近似线性相关，或系数行列式近似为零，但不绝对

* 系数矩阵元素量级差别很大且没有规则


```python

```
