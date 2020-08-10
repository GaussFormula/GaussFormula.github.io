# Local Space To World Space

## In fact, all you need is a matrix.
设：现有一个坐标系A，原点在<img src="https://latex.codecogs.com/gif.latex?(O_a,O_b,O_c)" title="(O_a,O_b,O_c)" /> ，其x轴、y轴和z轴在世界坐标系下的表示分别为<a href="https://www.codecogs.com/eqnedit.php?latex=(O_{x_x},O_{x_y},O_{x_z})" target="_blank"><img src="https://latex.codecogs.com/png.latex?(O_{x_x},O_{x_y},O_{x_z})" title="(O_{x_x},O_{x_y},O_{x_z})" /></a>，<a href="https://www.codecogs.com/eqnedit.php?latex=(O_{y_x},O_{y_y},O_{y_z})" target="_blank"><img src="https://latex.codecogs.com/png.latex?(O_{y_x},O_{y_y},O_{y_z})" title="(O_{y_x},O_{y_y},O_{y_z})" /></a>， <a href="https://www.codecogs.com/eqnedit.php?latex=(O_{z_x},O_{z_y},O_{z_z})" target="_blank"><img src="https://latex.codecogs.com/png.latex?(O_{z_x},O_{z_y},O_{z_z})" title="(O_{z_x},O_{z_y},O_{z_z})" /></a>。显然，作为一个坐标系，其x轴、y轴和z轴是互相垂直的。
## 假设现在有一个在世界坐标系中的点，它在上述坐标系A的表示应该是怎样的呢？
现在，我们需要在坐标系A的语境下来表示这个点。
<br>对于坐标系A来说，世界坐标系下的向量<img src="https://latex.codecogs.com/gif.latex?(O_{x_x},O_{x_y},O_{x_z})" title="(O_{x_x},O_{x_y},O_{x_z})" /> 正是坐标系A下的x轴，为了简单，可以将它假定为一个单位向量，即坐标系A下的<img src="https://latex.codecogs.com/gif.latex?(1,0,0)" title="(1,0,0)" />。
<br>假设存在一个矩阵M，这个矩阵有三个特点：
<br>能够与世界坐标系下的<img src="https://latex.codecogs.com/gif.latex?(O_{x_x},O_{x_y},O_{x_z})" title="(O_{x_x},O_{x_y},O_{x_z})" /> 相乘得到坐标系A下的<img src="https://latex.codecogs.com/gif.latex?(1,0,0)" title="(1,0,0)" />，即坐标系A下的x轴<br>
能够与世界坐标系下的<img src="https://latex.codecogs.com/gif.latex?(O_{y_x},O_{y_y},O_{y_z})" title="(O_{y_x},O_{y_y},O_{y_z})" /> 相乘得到坐标系A下的<img src="https://latex.codecogs.com/gif.latex?(0,1,0)" title="(0,1,0)" />，即坐标系A下的y轴<br>
能够与世界坐标系下的<img src="https://latex.codecogs.com/gif.latex?(O_{z_x},O_{z_y},O_{z_z})" title="(O_{z_x},O_{z_y},O_{z_z})" />相乘得到坐标系A下的<img src="https://latex.codecogs.com/gif.latex?(0,0,1)" title="(0,0,1)" />，即坐标系A下的z轴<br>
显然该矩阵M=<img src="https://latex.codecogs.com/gif.latex?\begin{bmatrix}&space;O_{x_x}&space;&&space;O_{x_y}&space;&&space;O_{x_z}\\&space;O_{y_x}&space;&&space;O_{y_y}&space;&&space;O_{y_z}\\&space;O_{z_x}&space;&&space;O_{z_y}&space;&&space;O_{z_z}&space;\end{bmatrix}" title="\begin{bmatrix} O_{x_x} & O_{x_y} & O_{x_z}\\ O_{y_x} & O_{y_y} & O_{y_z}\\ O_{z_x} & O_{z_y} & O_{z_z} \end{bmatrix}" />
<br>世界坐标系下的任何一个向量，在转为列矩阵并与矩阵M相乘之后，就得到了其在坐标系A下的表示。
