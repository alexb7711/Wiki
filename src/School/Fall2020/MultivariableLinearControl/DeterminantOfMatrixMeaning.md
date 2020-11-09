[What does the determminant of a matrix mean?](https://www.quora.com/What-does-the-determinant-of-a-matrix-mean?share=1)
First, let's examine what matrices "really are": When you multiply a matrix by the coordinates of a point, it gives you the coordinates of a new point. In this way, we can think of a matrix as a transformation which turns points in space into different points in space. And this is what matrix arithmetic is all about: matrices represent transformations (specifically, so-called "linear" transformations).

The determinant of a transformation is just the factor by which it blows up volume (in the sense appropriate to the number of dimensions; "area" in 2d, "length" in 1d, etc.). If the determinant is 3, then it triples volumes; if the determinant is 1/2, it halves volumes, and so on.

(The one nuance to add to this is that we are actually speaking about "oriented" volume. That is, our transformation may or may not turn figures inside out (e.g., in 2d, it might turn clockwise into counterclockwise; in 3d, it might turn left-hands into right-hands). If it does turn figures inside out, its determinant is considered negative.)

So, for example, in 3d: any rotation has determinant 1 because it leaves volume unchanged. Scaling everything up by a factor of 2 has determinant  23  because that's the factor by which it increases volume. Projecting everything onto a plane has determinant 0, because it flattens everything to volume 0. Any reflection has determinant -1, because it turns everything inside out but otherwise leaves volume unchanged. And so on...

Finally, one useful observation: if you take a transformation which multiplies volume by, say, 5, and follow it up with a transformation which multiplies volume by 3, then overall, volume will multiply by 5 * 3. Multiplying matrices amounts to chaining transformations end-to-end in this manner, so the determinant of a product of matrices is the product of their determinants.

[The reason a linear transformation has to blow up all regions' volumes by the same factor, should you care, is this: You can always think of any region as made up of lots of tiny regions, all identical except for their position. Each of these tiny regions is transformed in the same exact way except for position (this is the "linearity"), so the big region blows up by the same factor as each of the tiny regions. So, you can think of the determinant as the amount by which your favorite tiny shape scales in volume, and rest assured that all other regions scale by the same factor as well.]