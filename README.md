Download Link: https://assignmentchef.com/product/solved-comp-2210-assignment-3-identifying-line-segments-in-2d-data
<br>
This assignment will explore an example <em>feature extraction </em>problem. Feature extraction is a subproblem of pattern recognition and is also used in areas such as statistical analysis, computer vision, and image processing. For example, an image processing problem may use a feature extraction algorithm to identify particular shapes or regions in a digitized image.

In this assignment, we’re going to focus on a very simple feature extraction problem: Given a set of points in two-dimensional space, identify every subset of four or more points that are <em>collinear</em>. For example, given the set of points depicted in Figure 1, your program would detect the three groups of collinear points




<table>

 <tbody>

  <tr>

   <td width="35"></td>

  </tr>

  <tr>

   <td></td>

   <td></td>

  </tr>

 </tbody>

</table>

as depicted by the line segments in Figure 2.

Figure 1: A set of 13 points.




Figure 2: Three collinear groups identified.




As always, we want our solution to be useful at scale. For example, Figure 3 plots ⇠100,000 points and Figure 4 shows the 34 collinear groups identified by blue line segments. Each collinear group in Figure 4 is composed of far more than four points; four is just the minimum number of points to qualify for the collinear pattern that we’re looking for. In the general problem statement we will refer to line segments instead of collinear groups, where each line segment must contain at least four points.

Problem Statement: Given a set of <em>N </em>distinct points in Quadrant I of the Cartesian plane, identify every line segment that connects a subset of four or more of the points. Each point will be specified as an (<em>x,y</em>) pair where <em>x </em>and <em>y </em>are non-negative int values. For example, the thirteen points in Figures 1 and 2 are: (1, 7), (2, 2), (2, 5), (3, 1), (4, 4), (5, 3), (5, 6), (6, 6), (7, 1), (7, 3), (7, 4), (7, 9), (8, 8).

You must solve this problem in terms of the classes and methods described in the following sections.

1

Figure 3: A set of ⇠100,000 points.

<h1>The <strong>Point </strong>class</h1>




Figure 4: 34 collinear groups identified.




You must create an immutable<a href="#_ftn1" name="_ftnref1"><sup>[1]</sup></a> data type Point that represents a point in Quadrant I of the Cartesian plane. A shell of the Point class is provided for you, and you must meet the requirements specified in this document and the provided source code comments.

Some fields and methods have been completed for you and must not be changed. Some methods have incomplete bodies and you must complete them yourself. You may add any number of private methods that you like, but you may not add any public method or constructor, nor may you change the signature of any public method or constructor. You may not add any fields to this class.

A few aspects of the Point class are described in more detail below.

The <strong>compareTo </strong>method.

This method must compare points by y-coordinates and then, if needed, by x-coordinates. Thus, the invoking point (<em>x</em><sub>0</sub><em>,y</em><sub>0</sub>) is less than the parameter point (<em>x</em><sub>1</sub><em>,y</em><sub>1</sub>) if and only if either <em>y</em><sub>0 </sub><em>&lt; y</em><sub>1 </sub>or if <em>y</em><sub>0 </sub>= <em>y</em><sub>1 </sub>and <em>x</em><sub>0 </sub><em>&lt; x</em><sub>1</sub>. For example, by this <em>natural order </em>of points, (0, 1) is less than (0, 2), (7, 1) is less than (5, 3), and (3, 0) is less than (4, 0). (See Figure 5.) Two points are equal if and only if <em>y</em><sub>0 </sub>= <em>y</em><sub>1 </sub>and <em>x</em><sub>0 </sub>= <em>x</em><sub>1</sub>. This is consistent with the equals method, which is provided for you and must not be changed.

The <strong>slopeTo </strong>method.

This method must return the slope between the invoking point (<em>x</em><sub>0</sub><em>,y</em><sub>0</sub>) and the parameter point (<em>x</em><sub>1</sub><em>,y</em><sub>1</sub>), which is given by the formula:

For example, for the point (3, 3), the slope to (1, 1) is 1.0, the slope to (4, 5) is 2.0, and the slope to (5, 2) is -0.5. (See Figure 6.)

Treat the slope of a horizontal line segment (e.g., {(1,3), (3,3)}) as positive zero<a href="#_ftn2" name="_ftnref2"><sup>[2]</sup></a>; treat the slope of a vertical line segment (e.g., {(3,3), (3,5)}) as positive infinity<sup>2</sup>; treat the slope of a degenerate line segment (between a point and itself, e.g., {(3,3), (3,3)}) as negative infinity<sup>2</sup>. (See Figure 6.)

The <strong>slopeOrder </strong>Comparator

This field of the Point class must compare two points by the slopes they make with the invoking point (<em>x</em><sub>0</sub><em>,y</em><sub>0</sub>). Thus, the point (<em>x</em><sub>1</sub><em>,y</em><sub>1</sub>) is less than the point (<em>x</em><sub>2</sub><em>,y</em><sub>2</sub>) if and only if

For example, if the invoking point is (3, 3), then (5, 2) is less than (1, 1), and (1, 1) is less than (4, 5).

(See Figure 6.)

1

0    1              2              3              4              5              6              7              1              2              3              4              5 <em>x      x</em>

Figure 5: Reference for Point natural order.                   Figure 6: Reference for Point slope and slope order

<h1>The <strong>Line </strong>Class</h1>

You must create a data type Line that models a line segment as a <em>set </em>of points. A set is an appropriate model since a point only appears once on a line segment and the order in which points are listed is irrelevant. That is, {(1,7), (4,4), (5,3), (7,1)} and {(4,4), (7,1), (1,7), (5,3)} each define the same line segment. However, note that Point has a total order defined so we will make a Line a <em>sorted set </em>of Points. This is convenient since it means that there is exactly one representation of a line segment – one with the points in ascending natural order. Thus, the line segment above would be represented as {(7,1), (5,3), (4,4), (1,7)}.

A shell of the Line class is provided for you, and you must meet the requirements specified in this document and the provided source code comments. Some fields and methods have been completed for you and must not be changed. Some methods have incomplete bodies and you must complete them yourself. You may add any number of private methods that you like, but you may not add any public method or constructor, nor may you change the signature of any public method or constructor. You may not add any fields to this class.

The field line in the Line class has been declared for you as a java.util.SortedSet. You must use TreeSet as the implementing class.

<h2>The compareTo method</h2>

This method must compare lines by first points and then, if needed, by last points. Thus, <em>line</em><sub>1 </sub><em>&lt; line</em><sub>2 </sub>if <em>line</em><sub>1</sub><em>.first &lt; line</em><sub>2</sub><em>.first </em>or <em>line</em><sub>1</sub><em>.first </em>= <em>line</em><sub>2</sub><em>.first </em>and <em>line</em><sub>1</sub><em>.last &lt; line</em><sub>2</sub><em>.last</em>. (See Figure 7 where <em>l</em><sub>1 </sub><em>&lt; l</em><sub>2 </sub><em>&lt; l</em><sub>3</sub>.) Two lines <em>line</em><sub>1 </sub>and <em>line</em><sub>2 </sub>are equal if and only if <em>line</em><sub>1</sub><em>.first </em>= <em>line</em><sub>2</sub><em>.first </em>and <em>line</em><sub>1</sub><em>.last </em>= <em>line</em><sub>2</sub><em>.last</em>. This is consistent with the equals method, which is provided for you and must not be changed.

5

2

Figure 7: Reference for Line natural order.

<h1>The <strong>Extractor </strong>Class</h1>

You must create a class Extractor that finds all line segments of four or more collinear points in provided data. A shell of the Extractor class is provided for you, and you must meet the requirements specified in this document and the provided source code comments. A few aspects of the Extractor class are discussed in more detail below.

The Constructors

The first constructor for the Extractor class takes a single parameter of type String. This parameter is a filename for a file of Point data formatted as follows: The first line of the file contains a single int value <em>N </em>that is the number of lines Point data that follow. Each of the following <em>N </em>lines contains two int values separated by one or more blanks. The first int is the <em>x </em>value of a Point and the second int is the <em>y </em>value of a Point. There may be lines of text past these first <em>N </em>+ 1 lines of data, but they should be ignored. A sample input file is shown below.

5

11000 11000 12000 10000 13000 10000 14000 10000 15000 10000

Instantiating an Extractor object with this data file would ensure that five distinct instances of the Point class are stored in a suitable data structure inside the new Extractor object.

The second constructor takes a Collection of points and creates an Extractor for this data.

<h2>The getLinesBrute method</h2>

This method implements a straight-forward, <em>brute force </em>approach to extracting the feature that we’re interested in. Since <em>any </em>combination of four distinct points that are collinear qualify as our feature, we can generate <em>all </em>combinations of four distinct points and check each combination to see if those four points are collinear. This brute force solution is a <em>combinatoric </em>approach to the problem: We generate all the combinations of <em>N </em>things taken four at a time and test each combination based on our feature criteria

(collinearity).

For example, let’s name the points in the given sample input file <em>p</em><sub>1 </sub>through <em>p</em><sub>5</sub>, as shown below.

5

11000 11000 (<em>p</em><sub>1</sub>)

12000 10000 (<em>p</em><sub>2</sub>)

13000 10000 (<em>p</em><sub>3</sub>)

14000 10000 (<em>p</em><sub>4</sub>)

15000 10000 (<em>p</em><sub>5</sub>)

The table below shows all the combinations of these five points taken four at a time, along with the result of testing each combination for collinearity. Note that to check if four points <em>p</em>, <em>q</em>, <em>r</em>, and <em>s </em>are collinear, we check whether the slope between <em>p </em>and <em>q</em>, between <em>p </em>and <em>r</em>, and between <em>p </em>and <em>s </em>are all equal.

<table width="186">

 <tbody>

  <tr>

   <td width="110">Combination</td>

   <td width="76">Collinear?</td>

  </tr>

  <tr>

   <td width="110"><em>p</em>1<em>,p</em>2<em>,p</em>3<em>,p</em>4</td>

   <td width="76">no</td>

  </tr>

  <tr>

   <td width="110"><em>p</em>1<em>,p</em>2<em>,p</em>3<em>,p</em>5</td>

   <td width="76">no</td>

  </tr>

  <tr>

   <td width="110"><em>p</em>1<em>,p</em>2<em>,p</em>4<em>,p</em>5</td>

   <td width="76">no</td>

  </tr>

  <tr>

   <td width="110"><em>p</em>1<em>,p</em>3<em>,p</em>4<em>,p</em>5</td>

   <td width="76">no</td>

  </tr>

  <tr>

   <td width="110"><em>p</em>2<em>,p</em>3<em>,p</em>4<em>,p</em>5</td>

   <td width="76"><em>yes</em></td>

  </tr>

 </tbody>

</table>

The advantage of this brute force approach is that it’s simple to code. In this assignment, the number of points being selected out of the set of <em>N </em>total points is fixed at four, so four nested for loops can be used to generate all the possible combinations. That’s also the problem with this brute force approach: four nested loops each dependent on <em>N </em>will have <em>O</em>(<em>N</em><sup>4</sup>) time complexity.

For a given number of points <em>N</em>, we know exactly how many combinations of four points will be computed. That is given by <em><sup>N</sup></em><em><sub>k </sub></em>where <em>k </em>= 4.

For our example above, this would give <u><sup>5!</sup></u><sub>4! </sub>= 5 combinations. If the input had 10 points, the brute force solution would have to test <sub>4!</sub> different combinations of four points. For <em>N </em>= 20, the brute force solution would generate and test 4845 combinations of four points. For <em>N </em>= 1000, over <em>41 billion </em>combinations of four points would be generated and tested by our program. You can see how this escalates very quickly and the brute force solution becomes impractical to apply as the problem size scales up.

<h2>The getLinesFast method</h2>

We can solve this problem much more efficiently if we use sorting as part of our solution. In a group of collinear points, the slope that any two points make with respect to each other is, by definition, the same. For example, in Figure 7 the slope between any two points on <em>l</em>1 is positive 1, the slope between any two points on <em><sub>l</sub></em>2 is 1.0, and the slope between two points on <em><sub>l</sub></em>3 is -1.0. Given a set of points, if we select a reference point and sort all other points with respect to the slope they make with that reference point, then all points mutually collinear with the reference point would be “duplicates” with respect to that ordering and would therefore be in arranged in continguous groups.

For example, here are the points in Figure 7.

(1, 6)      (2, 2)       (2, 5)       (3, 1)      (3, 2)       (3, 3)       (3, 4)      (3, 5)       (4, 3)       (4, 4)      (5, 2)       (5, 5)

And here are the points in Figure 7 sorted with respect to the slope they make with (3, 4).

Note how all the points that are mutually collinear with (3, 4) are now in contiguous groups (<em>l</em><sub>1 </sub>is highlighted in light red and <em>l</em><sub>3 </sub>is highlighted in light blue). Underneath each point is the slope it makes with (3, 4)<a href="#_ftn3" name="_ftnref3"><sup>[3]</sup></a>. Similarly, here are the points in Figure 1.

(1, 7)      (2, 2)       (2, 5)       (3, 1)      (4, 4)       (5, 3)       (5, 6)      (6, 6)       (7, 1)       (7, 3)      (7, 4)       (7, 9)       (8, 8)

And here are the points in Figure 1 sorted with respect to the slope they make with (7, 1).

All the points that are mutually collinear with (7, 1) are now in contiguous groups (highlighted). Underneath each point is the slope it makes with (7, 1).

We can now apply the following strategy to solve the problem.

<ol>

 <li>Sort the <em>N </em>points with respect to the slope that they make with one of the points <em>p</em>.</li>

 <li>Scan the sorted points to find all groups of three or more consecutive points having the same slope to <em>p</em>. Each such group is collinear with <em>p </em>and thus, together with <em>p</em>, form a line segment of at least four points.</li>

 <li>Repeat steps 1 and 2 for the remaining <em>N </em>1</li>

</ol>

How much faster is this sort-and-scan approach? We can sort in <em>O</em>(<em>N </em>log<em>N</em>) time and the subsequent scan is <em>O</em>(<em>N</em>). We have to perform these operations for all <em>N </em>points, so the total cost of this <em>sort and scan </em>approach is <em>N </em>⇥ (<em>NO</em>log(<em>N</em>2<em>N</em>log+<em>NN</em>)) =<em>ON</em>(<em>N</em>2 log4), and the clock-time di<em>N </em>+ <em>N</em>2 which is <em>O</em>(<em>N</em>fference is dramatic. Problem sizes that are2 log<em>N</em>). This is a significant asymptotic

improvement since

impractical for the brute force solution are solved quickly (or at least in a reasonable amount of time) by this sort-and-scan solution.

But there is an additional benefit of this approach: We are no longer limited to identifying only four-point line segments. We can now identify <em>maximal </em>line segments of four or more collinear points.

<h2>Notes and other requirements</h2>

Here are a couple of extra requirements plus a few things to keep in mind.

<ul>

 <li>Start this one early<sub>this assignment. Read this handout carefully. Ask questions of your TA and of me. Ask questions on</sub>. There’s more reading, thinking, and up-front understanding to take care of on</li>

</ul>

Piazza. Start early and be proactive.

<ul>

 <li>You’ve been provided with shells of the<em>that has already been done for you</em>. Point, Line, and Extractor classes. <em>Don’t modify anything</em></li>

 <li>Start by completing the remaining methods of the<sub>List </sub>or <sub>Extractor </sub>class before this is complete and correct, since both depend onPoint class. There’s no <em>point</em><a href="#_ftn4" name="_ftnref4"><sup>[4]</sup></a> in attempting the<sub>Point</sub>.</li>

 <li>Complete theboth <sub>Line </sub>andLine<sub>Point</sub>class after, you must have these working first.Point but before Extractor. Again, since Extractor depends on</li>

 <li>When you begin work on theshorter and easier to get correct quickly. Once you are satisfied thatExtractor class, start with the getLinesBrutegetLinesBrutemethod. This isis correct, turn your attention to getLinesFast.</li>

 <li>Inexample, if the line segmentgetLinesFast, do not print subsegments of lines containing five or more collinear points. For<em><sub>p </sub></em>! <em><sub>q </sub></em>! <em><sub>r </sub></em>! <em><sub>s </sub></em>! <em><sub>tp</sub></em>exists in the data, you must identify it but you must! <em><sub>q </sub></em>! <em><sub>r </sub></em>! <em><sub>s</sub></em>. not identify any four-point subsegment such as</li>

</ul>

<a href="#_ftnref1" name="_ftn1">[1]</a> This means that once you create a Point you can’t change its <em>x </em>or <em>y </em>value. Thus, the class is final, the fields are final and private, and there are no setter methods.

<a href="#_ftnref2" name="_ftn2">[2]</a> See the Java documentation of the Double class for a discussion of <em>positive zero</em>, <em>positive infinity</em>, and <em>negative infinity</em>.

<a href="#_ftnref3" name="_ftn3">[3]</a> Now do you see why we defined the slope of degenerate lines as negative infinity?

<a href="#_ftnref4" name="_ftn4">[4]</a> Sorry; couldn’t resist. Here’s more: www.punoftheday.com