02-CATransform3D

  
layer的CATransform3D属性.只有旋转的时候才可以看出3D的效果.

旋转  
x,y,z分别代表x,y,z轴.CATransform3DMakeRotation\(M\_PI, 1, 0, 0\);

平移  
CATransform3DMakeTranslation\(x,y,z\)  
缩放  
CATransform3DMakeScale\(x,y,z\);

可以通过KVC的 式进 设置属性.  
但是CATransform3DMakeRotation它的值,是 个结构体,所以要把结构转成对象.  
NSValue \*value = \[NSValue valueWithCATransform3D:CATransform3DMakeRotation\(M\_PI, 1, 0, 0\)\];\[\_imageView.layer setValue:value forKeyPath:@"transform.scale"\];

什么时候KVC?  
当需要做 些快速缩放,平移,维的旋转时KVC.  
如: \[\_imageView.layer setValue:@0.5 forKeyPath:@"transform.scale"\];快速的进 缩放.后forKeyPath属性值不是乱写的.苹果 档当中给了相关的属性.
