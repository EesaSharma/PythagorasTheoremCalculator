# PythagorasTheoremCalculator
A simple Pythagoras Theorem calculator in JavaScript.
Imagine we have two points on a coordinate plane:
We can use the equation of a line to find all the y points between these two points as we move along the x axis:
y = mx + b (where m is the slope: rise/run and b is the y-intercept - the point at which the line crosses the y axis)
The slope tells us the steepness or slant of the line and the y-intercept tell us where the line intersects the y-axis
Without knowing the y-intercept, we would only know the slope of the line, which tells us how the line is slanting but not where it is located on the y-axis.
Essentially, for every x position change, we need to find the new y coordinate and we can do this with the previous equation and values we find.
We can find the slope by finding the ratio between the difference in our y2 and y1 values and our x2 and x1 values:
m = (y2-y1) / (x2-x1);
In the case of our points above: 300-100 / 300-100 or 200/200 or 1/1 or 1
So for every change in x, there is an equal change in y.
A horizontal line would have a 0 slope and a vertical line would involve division by zero and would be undefined as we'll see soon.
Horizontal line: 100 - 100 / 300 - 100 or 0 / 200 or 0
Vertical line: 300 - 100 / 100 - 100 or 200 / 0 or undefined
For the y-intercept, we're just rearranging the line equation so instead of y = mx + b, we subtract mx from both sides to isolate b:
y - mx = b 
or
b = y - mx
More specifically for our program:
b = y1 - m * x1;
All of this code can go in the setup as we're simply generating a line segment one time, but let's make this more dynamic so we can see some problems that arise.
x1 = width/2;
y1 = height/2;
function draw() {
  background(220);
  x2 = mouseX;
  y2 = mouseY;
  m = (y2 - y1) / (x2 - x1);
  b = y1 - m * x1;
  stroke('#ff0000');
  for (let x = x1; x <= x2; x++) {
    y = m * x + b;
    point(x, y);
   }
}
This code will produce a line segment that starts at the middle of the canvas and ends at the mouse position.
We can update the loop:
for (let x = min(x1, x2); x <= max(x1, x2); x++) {
This will get the lower and higher value of each so the line will work on the right or left sides of the canvas.
Here's a more detailed breakdown of the Bresenham's Line Algorithm:
Start by defining the two endpoints of the line, (x1, y1) and (x2, y2). Calculate the differences in x and y coordinates: dx = x2 - x1 and dy = y2 - y1.
Determine the primary axis, which is the axis with the larger difference. If dx > dy, the primary axis is the x-axis; otherwise, it's the y-axis.
Calculate the error term, which is the difference between the primary and secondary axes. If the x-axis is primary, the error term is 2 * dy - dx; if the y-axis is primary, the error term is 2 * dx - dy.
Initialize the current coordinates (x, y) to the starting point (x1, y1), and set the initial error to 0.
a. Color the pixel at the current coordinates (x, y).
b. Move one step in the primary axis direction (increment x if x-axis is primary, or increment y if y-axis is primary).
c. Update the error by adding the difference in the secondary axis (2 * dy if x-axis is primary, or 2 * dx if y-axis is primary).
d. If the error is greater than or equal to the primary axis difference (dx if x-axis is primary, or dy if y-axis is primary), move one step in the secondary axis direction (increment y if x-axis is primary, or increment x if y-axis is primary) and subtract the primary axis difference from the error (subtract 2 * dx if x-axis is primary, or subtract 2 * dy if y-axis is primary).
e. Repeat steps 5a-5d until the endpoint (x2, y2) is reached.
Bresenham's Line Algorithm ensures that the drawn line appears smooth and continuous on the grid, while using only integer arithmetic, making it efficient and easy to implement in computer graphics applications.
The p5.js library uses a more advanced graphics rendering system than the Bresenham's Line Algorithm. While Bresenham's Line Algorithm is an important concept to understand and is still used in some low-level graphics applications, modern graphics libraries, including p5.js, often rely on hardware acceleration and more advanced rendering techniques.
p5.js uses the HTML5 canvas API for rendering 2D graphics, which in turn uses the computer's GPU to perform drawing operations. The line function in p5.js eventually calls the native canvas API function stroke to draw the line, which is handled by the browser's rendering engine.
The actual algorithm used by the canvas API for drawing lines might vary depending on the browser, operating system, and hardware, but it is usually more advanced than the Bresenham's Line Algorithm to accommodate anti-aliasing, sub-pixel rendering, and other features that provide smoother and more visually appealing graphics
While Bresenham's Line Algorithm is a foundational technique for drawing lines on a grid, the p5.js line function uses the more advanced HTML5 canvas API for rendering graphics, which is typically backed by hardware acceleration and optimized rendering techniques.
