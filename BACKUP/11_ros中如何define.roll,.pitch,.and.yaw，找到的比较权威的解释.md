# [ros中如何define roll, pitch, and yaw，找到的比较权威的解释](https://github.com/huaizhixu/Huaizhi-Blog/issues/11)

To define roll, pitch, and yaw in linear systems, we first need to establish the three primary axes: X, Y, and Z.


![Roll-Pitch-Yaw](https://user-images.githubusercontent.com/108015790/210919732-4d3906fb-cb5e-49c7-8fa4-9116e36cdca1.jpg)


The two axes of the horizontal plane are typically defined as X and Y, with the X axis being in the direction of motion. The Y axis is orthogonal (perpendicular) to the direction of motion and is also in the horizontal plane. The Z axis is orthogonal to both the X and Y axes, but it is located in the vertical plane. (To find the positive direction of the Z axis, use the [right-hand rule](https://mathworld.wolfram.com/Right-HandRule.html): point the index finger in the direction of positive X, then curl it in the direction of positive Y, and the thumb will indicate positive Z.)

___

_In multi-axis systems, the direction of travel of the bottom axis is typically defined as the X axis. If the next axis above it is also horizontal, that axis is defined as Y, and the vertical axis (even if it is the second axis, directly on top of X), is defined as the Z axis._