# Vector math

Vector - expression of direction and length. 
```ts
const vector = vec(x, y, z);
vector.length
```

## Operations with vectors

### Addition
![image](https://user-images.githubusercontent.com/7611372/202461509-4fc881d6-ad2c-4e74-b994-fb48d59ac6fb.png)


```js
v1 = vec(1, 0, 0);
v2 = vec(0, 1, 0);

/*
v3.x = v1.x + v2.x
v3.y = v1.y + v2.y
v3.z = v1.z + v2.z
*/

v3 = v1 + v2;
// 1, 1, 0
```

### Subtraction
Basically, just addition with negative values.

### Multiplication / division
Changing length of vector
```js
v1 = vec(10, 10, 0);

v2 = v1 / 10; // or v1 * 0.1
// 1, 1, 0
```

### Normalization and magnitude
Normalized vector which is 1 unit length.

Magnitude - length/size of vector.

```js
v = vec(5, 5, 5)
v.length // 8.66025

v1 = normalize(v)// 0.57735, 0.57735, 0.57735
v1.length // 1
```

### Dot product

Dot product is projection of length of vector to another vector.

![image](https://user-images.githubusercontent.com/7611372/202464977-18c9a3d6-ee87-4491-a1a4-5530a85ac782.png)

```js
v1 = vec(1, 0, 0);
v2 = vec(0, 1, 0);
v3 = vec(-1, 0, 0);

dot(v1, v2); // 0
dot(v1, v1); // 1
dot(v1, v3); // -1
```

### Cross product

Cross product calculates perpendicular vector to another two vectors.

![image](https://user-images.githubusercontent.com/7611372/202467877-50be9ed2-7171-4c9b-923a-eff29785cb2d.png)

```js
v1 = vec(1, 0, 0);
v2 = vec(0, 1, 0);
v3 = cross(v1, v2); // 0, 0, 1
```

# Trigonometry

## Radians/degrees

PI = length of circle divided by its diameter.

```js
PI rad = 180 degrees
2PI = 360
```

### Conversion

```js
rad = deg * PI / 180

deg = rad * 180 / PI
```

## `sin`, `cos` & `tan`

![image](https://user-images.githubusercontent.com/7611372/202475393-f1efca6d-5d7c-4484-af3b-961bb0c6097d.png)

### `secant`, `cosecant` & `cotan`
Just inverted `sin`, `cos` and `tan`.

```js
secant   = 1/sin(rad)
cosecant = 1/cos(rad)
cotan    = 1/tan(rad)
```

### Unit circle 

Complex numbers can be used to represent rotations in a 2D plane.

To see how this works, imagine a point on the plane with coordinates (x,y). We can represent this point as a complex number z = x + iy, where i is the imaginary unit.

Now, let's consider a rotation of angle θ around the origin. We can represent this rotation as the complex number w = cos(θ) + i sin(θ), which is also known as Euler's formula.

To rotate the point (x,y) by θ, we multiply z by w:

z' = zw

If we expand this multiplication using the distributive law, we get:

z' = (x + iy)(cos(θ) + i sin(θ))

z' = xcos(θ) - ysin(θ) + i(xsin(θ) + ycos(θ))

The real part of z' represents the new x-coordinate of the rotated point, and the imaginary part represents the new y-coordinate.

So, by using complex numbers to represent rotations, we can easily perform rotations in a 2D plane using simple multiplication and trigonometric functions.

Similarly, quaternions can be used to represent rotations in 3D space, where they allow for more complex rotations and orientations than complex numbers can represent in 2D space.

![image](https://user-images.githubusercontent.com/7611372/202477157-989816ad-88f8-4cd3-a75c-d17688e4ceb7.png)

```js
x = radius * cos(sampled_angle);
y = radius * sin(sampled_angle);
```

<img width="300" alt="image" src="https://user-images.githubusercontent.com/7611372/202478478-714d452d-1c82-4427-b0e8-cae6fd4ceb91.png">

```js 
// draw circle
for (let i = 0; i < 360; i++) {
  const irad = degToRad(i);
  pos = r * vec(cos(irad), sin(irad));
  point(pos);
}
```

<img width="539" alt="image" src="https://user-images.githubusercontent.com/7611372/202481295-56e1d56f-d00e-4ffc-9c61-ecc734b82d9d.png">

```js
// draw wave
for (let i = 0; i < 360; i++) {
  const irad = degToRad(i);
  pos = amp * vec(irad, sin(irad));
  point(pos);
}
```

## Inverse trigonometry (to estimate angle value)

Cartesian coordinates are a way to describe a point on a plane using its x and y coordinates. Polar coordinates, on the other hand, use a point's distance from the origin (r) and the angle it makes with the positive x-axis (θ) to describe its location.

Inverse trigonometric functions, such as arctan and arcsin, can be used to calculate the angle (θ) that a point makes with the positive x-axis given its x and y coordinates. Once you have the angle, you can use trigonometric functions (sine, cosine, tangent) to calculate the distance (r) of the point from the origin.

By converting a point from Cartesian coordinates to polar coordinates, you can easily perform rotations by changing the angle (θ) and then convert the point back to Cartesian coordinates to see its new x and y coordinates. This is useful for working with geometric objects in two-dimensional space, such as rotating shapes or positioning objects relative to one another.

<img width="264" alt="image" src="https://user-images.githubusercontent.com/7611372/202486524-14449b98-7cd9-434d-a8ec-5984dbe82fd6.png">


```js 
angle = asin(b/a) // sin (0 - 90)
angle = acos(c/a) // cos (0 - 180)
angle = atan(b/c) // tan (0 - 90) =/
```

### Atan2 to estimate 0 - 360

The atan2 function is a variant of the inverse tangent function that is used to compute the angle of a point relative to the origin (0, 0) in a two-dimensional coordinate system. Unlike the standard inverse tangent function, which only gives the angle of a point on the positive x-axis, the atan2 function can compute the angle of a point for any position in the plane.

```js
angle = atan2(b, c); // atan2(y, x)
```

# Quaternion

Quaternions are mathematical objects that extend the concept of complex numbers to four dimensions. They are commonly used in computer graphics to represent rotations and orientations in 3D space.

The following operations can be performed with quaternions:

1. **Multiplication**: The product of two quaternions results in a new quaternion that represents a **combination of their rotations**. Quaternion multiplication is not commutative, meaning that the order in which quaternions are multiplied matters.
2. **Addition and subtraction**: The addition and subtraction of quaternions result in a new quaternion with the same components as the original quaternions. It allows us to smoothly interpolate between different rotations. For example, if we want to animate an object moving from one orientation to another, we can use quaternion addition to smoothly transition between the two rotations over time.
3. **Conjugation**: The conjugate of a quaternion is obtained by negating the imaginary components. The conjugate of a quaternion represents the same rotation as the original quaternion, but in the opposite direction.
4. **Normalization**: A quaternion can be normalized by dividing each of its components by its magnitude. Normalizing a quaternion ensures that it represents a valid rotation.
5. **Inversion**: The inverse of a quaternion is obtained by dividing its conjugate by its magnitude. The inverse of a quaternion represents the inverse rotation of the original quaternion.

### Houdini

```vex
v@v = {1, 0, 0};
vector4 q = quaternion($PI/2, {0, 1, 0});

@N = qrotate(q, @v);
```

<img width="341" alt="image" src="https://user-images.githubusercontent.com/7611372/202493177-c346cd5e-46f5-4ff5-a4d2-ad28c2c7509f.png">


### Three.js

```js
const quaternion = new THREE.Quaternion();
quaternion.setFromAxisAngle( new THREE.Vector3( 0, 1, 0 ), Math.PI / 2 );

const vector = new THREE.Vector3( 1, 0, 0 );
vector.applyQuaternion( quaternion );
```



### Dihedral

A `dihedral` operation is a type of symmetry that involves a reflection across a plane, followed by a rotation about an axis that is perpendicular to that plane.

To apply a dihedral operation to a vector, you can follow these steps:

1. Determine the plane of reflection and the axis of rotation. This is important because it will determine the direction of the reflection and the amount of rotation.

2. Reflect the vector across the plane of reflection. This can be done by multiplying the vector by a matrix that represents the reflection.

3. Rotate the vector about the axis of rotation. This can be done by multiplying the vector by a matrix that represents the rotation.

4. Repeat the reflection and rotation steps as needed to achieve the desired dihedral symmetry.

```
vector v1 = {1, 0, 0};
vector v2 = {0, 1, 0};

vector4 q = dihedral(v1, v2);

@P = qrotate(q, @P);

```
<img width="428" alt="image" src="https://user-images.githubusercontent.com/7611372/202494756-a5dd486e-58e0-4fd4-b8c3-90a5ef8a9b87.png">

# Matrices / Transformations

Matrices are used to represent geometric transformations such as translation, rotation, scaling, and skewing. Matrices allow us to perform these transformations efficiently and accurately in 3D space.

1. **Addition and subtraction**: We can add or subtract matrices of the same size to combine or separate transformations.
2. **Multiplication**: We can use matrix multiplication to apply multiple transformations to an object, such as translating it, rotating it, and scaling it. We can also use matrix multiplication to transform vectors and perform projections.
3. **Identity matrix**: An identity matrix is a matrix with 1's on the main diagonal and 0's elsewhere. It represents no transformation and can be used to reset or initialize matrices.
4. **Inverse matrix**: The inverse of a matrix can be used to undo a transformation. For example, if we have translated an object using a matrix, we can use the inverse of the matrix to move the object back to its original position.
5. **Transpose**: The transpose of a matrix is used to switch its rows and columns. This can be useful when performing certain operations, such as transforming normals.
6. **Determinant**: The determinant of a matrix is a scalar value that can be used to compute its inverse and to measure the scaling factor of a transformation.
7. **Eigenvalues and eigenvectors**: Eigenvalues and eigenvectors are used to represent the stretching and shrinking of an object in different directions.
8. **Orthogonalization**: Orthogonalization is the process of creating an orthogonal matrix, which is a matrix where the columns and rows are perpendicular to each other. Orthogonal matrices preserve distances and angles, for maintaining the shape and size of an object.

### Identity matrix

```
1 0 0 0
0 1 0 0
0 0 1 0
0 0 0 1
```

```vex
matrix m = ident();
```

```js
const m = new THREE.Matrix4();
```

### Determinant

Used to check is matrix has inverse matrix variant.

### Inverse

Used to reverse transformations.

The inverse of the matrix representing the transformation is the matrix that undoes the transformation. For example, the inverse of a matrix that represents a rotation in 3D space is the matrix that represents the opposite rotation.

To find the inverse of a matrix, we need to find a matrix that, when multiplied by the original matrix, yields the identity matrix.

In general, finding the inverse of a matrix can be computationally expensive, especially for large matrices. Therefore, in computer graphics, it is often more efficient to use the transpose of a matrix to represent the inverse of a transformation. This is because the transpose of a matrix is often the matrix that represents the inverse of the original transformation.

```
@P *= inverse(4@mat);
```

### Transpose

Swap rows with columns.

Transpose of a rotation matrix is the same as its inverse. This is because rotation matrices are orthogonal matrices, which means that the transpose of a rotation matrix is also its inverse.

If a matrix includes a translation component in addition to the rotation component, then the transpose of the matrix is not the same as its inverse. In this case, a simplified inversion algorithm can be used, involving a transpose and an adjustment of the translation term. 

In general, to invert a matrix that encodes complex transformations, a full inversion function must be used. This can be computationally expensive, especially for large matrices.

### Multiplication scalar

Just each number multiplied.

```
[A A A]       [kA kA kA]
[A A A] * k = [kA kA kA]
[A A A]       [kA kA kA]
```

### Multiplication vector

Same as multiplication with matrix, aka **column matrix**.

```
// column based (OpenGL)
M*vec = res

// row based (DirectX, Houdini)
vec*M = res
```

### Multiplication matrix

Operation order is matter. TRS ≠ RTS ≠ SRT.

**ROW x COLUMN**

```
[a b] * [e f] = [a*e + b*g][a*f + b*h]
[c d]   [g h]   [c*e + d*g][c*f + d*h]
```

#### Identity matrix

```
[a b] * [1 0] = [a b]
[c d]   [0 1]   [c d]
```

### Transformation matrix

To apply a transformation to a point, the point is represented as a column vector, and the transformation matrix is multiplied by the vector to produce a new vector representing the transformed point. The specific elements of the transformation matrix determine the type of transformation that is applied. For example, a translation transformation matrix will contain elements that specify the distances by which the point should be moved in the x, y, and z directions.

```js
// Position

1 0 0 0
0 1 0 0
0 0 1 0
x y z 1

// Rotation
r r r 0
r r r 0
r r r 0
0 0 0 1

// Scale

x 0 0 0
0 y 0 0
0 0 z 0
0 0 0 1
```


