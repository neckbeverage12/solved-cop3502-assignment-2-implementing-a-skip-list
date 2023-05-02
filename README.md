Download Link: https://assignmentchef.com/product/solved-cop3502-assignment-2-implementing-a-skip-list
<br>
Build a <em>skip list </em>data structure to support the traversal, searching, addition, and deletion of integers from a <em>skip list</em>. This implementation will support building a <em>skip list </em>to support integers in the range of 0 to 5,000. The objective of this assignment requires the reading of an input file which contains commands and data to build a <em>skip list </em>containing integers using commands to insert, search, delete, and print a <em>skip list</em>.

2             Requirements

Read the input file formatted as follows. The input file will contain at least one command per line, either insert, delete, search, print, or quit. These are defined in detail below. And if appropriate, a second parameter may be required. The second parameter, if appropriate, will always be an integer for this assignment.

The commands are shown in the table below:

<table width="461">

 <tbody>

  <tr>

   <td width="86">Command</td>

   <td width="94">Description</td>

   <td width="281">Parameter(s)</td>

  </tr>

  <tr>

   <td width="86"><strong>i</strong></td>

   <td width="94">Insert</td>

   <td width="281">expects a space, followed by an integer</td>

  </tr>

  <tr>

   <td width="86"><strong>s</strong></td>

   <td width="94">Search</td>

   <td width="281">expects a space, followed by an integer</td>

  </tr>

  <tr>

   <td width="86"><strong>d</strong></td>

   <td width="94">Delete</td>

   <td width="281">expects a space, followed by an integer</td>

  </tr>

  <tr>

   <td width="86"><strong>p</strong></td>

   <td width="94">Print</td>

   <td width="281"><strong>does not </strong>expect any additional data</td>

  </tr>

 </tbody>

</table>

Table 1: Input File Commands

<h2>2.1           Design Constraints</h2>

The input file(s) provided will have the following properties.

<ol>

 <li>Each record in the input file will consist of a command, described above, appropriately followed by an integer.</li>

 <li>There is not a <em>maximum </em>number of skip levels.</li>

 <li>The test input integers will be within the range of 1 to 5,000.</li>

 <li>There is no requirement for persistence. The data in the <em>skip list </em>does not need to be stored or archived on disk before the program exits.</li>

</ol>

<h2>2.2           Commands</h2>

<h3>2.2.1             Insert</h3>

The insert command uses the single character <strong>i </strong>as the command token. The command token will be followed by a single space, then an integer. This integer will then be inserted into the <em>skip list</em>. Note that a <em>skip list </em>requires that data be inserted into the <em>skip list </em>in ascending order.

<ol>

 <li>Insertion requires that the specified integer will be inserted at the lowest level of the <em>skip list </em>and will be appropriately connected with the preceding integer and the next integer on the lowest level. For example inserting a 5 between a 3 and a 7 would result in the the 3 becoming the preceding integer and 7 becoming the next integer relative the newly inserted 5.</li>

</ol>

<ul>

 <li>In the event that the inserted integer would be placed at either the <em>lowest </em>or <em>highest </em>rank, that is at the <em>lowest </em>or <em>highest </em>possible value for the lowest <em>skip list </em>level make sure that new <em>lowest </em>or <em>highest </em>rank integer is appropriately connected or represented as connected to either −∞ or +∞.</li>

</ul>

<ol start="2">

 <li>Insertion of an integer that requires a probabilistic mechanism to decide if this integer will also be promoted <em>to the next higher level </em>regardless of whether it is the <em>lowest </em>or <em>highest </em>rank integer. The method discussed in lecture is <em>flipping a fair coin</em>. The <em>flipping of a fair coin </em>can be emulated using the Random object in Java to generate a “random number” then taking that number <strong>modulo 2 </strong>to generate a <strong>1 </strong>or <strong>0</strong>. The optional seeding of the Random number generator will be the second command line parameter specified by an upper or lower case <strong>R </strong>. <em>In the event that the </em><em>R parameter is </em><em>not specified, seed the Random number generator with the integer </em><em>42. </em>The promotion method used to generate the test cases used a <strong>1 </strong>to represent <em>heads </em>and correspondingly a <strong>0 </strong>to represent <em>tails</em>. Each flip of the coin that produces a <em>heads </em>causes that integer to be promoted and appropriately linked into the <em>skip list</em>. This process is terminated when a <em>tails </em>has been “flipped”.</li>

 <li>In the event that the number to be inserted already exists in the <em>skipList </em>it can be <em>ignored </em>as there is no requirement for duplicate entries in this implementation.</li>

</ol>

<strong>Inputs </strong>i xx where <strong>xx </strong>is an integer between 1 and 5,000.

<strong>Outputs</strong>

N/A

<h3>2.2.2          Delete</h3>

The delete command uses the single character <strong>d </strong>as the command token. The command token will be followed by a single integer. In order to successfully delete an entry from the <em>skip list</em>, the integer must be found.

In the event that the <em>integer </em>cannot be found, the program will issue the error message xx integer not found – delete not successful, where xx is the specified integer. The program will recover gracefully to continue to accept commands.

Once the <em>integer </em>is found, it will be deleted from the <em>lowest </em>level, and any additional level(s) that integer had been promoted to upon insertion. <em>Remember to appropriately connect the previous and next values across all levels that contained the deleted integer. </em>(This command’s success can be verified by using the <em>print </em>command.)

<strong>Inputs </strong>d xx where <strong>xx </strong>is an integer between 1 and 5,000.

<h3>Outputs</h3>

<strong>Success </strong>xx deleted <em>:where xx is the integer being deleted</em>

<h3>Failure</h3>

xx integer not found – delete not successful <em>:where xx is the integer being deleted was not found</em>

<h3>2.2.3             Search</h3>

The search command uses the single character <strong>s </strong>as the command token. The command token will be followed by a single space, then the integer that is to be searched

The <em>search </em>command will take advantage of the <em>skip list </em>structure and implement the following algorithm. <em>A search for a target element begins at the head element in the top list, and proceeds horizontally until the current element is greater than or equal to the target. If the current element is equal to the target, it has been found. If the current element is greater than the target, or the search reaches the end of the linked list, the procedure is repeated after returning to the previous element and dropping down vertically to the next lower list.</em><a href="#_ftn1" name="_ftnref1"><sup>[1]</sup></a>

Upon completion of the search for the target integer, the following messages shall be output. <strong>Inputs </strong>s xx where <strong>xx </strong>is an integer between 1 and 5,000.

<h3>Outputs</h3>

<strong>Success </strong>xx found <em>:where xx is the integer being searched for</em>

<strong>Failure </strong>xx NOT FOUND <em>:where xx is the integer being searched for and was not found</em>

<h3>2.2.4          Print</h3>

The print command uses the single character <strong>p </strong>as the command token. This command will invoke the <em>printAll </em>function described in detail below.

This command is critical for verification of all the commands specified above.

<strong>Inputs </strong>p

<h3>Outputs</h3>

EUSTIS_SYSTEM_PROMPT$java Hw02 H2in-a1.txt bs123456;3.141592653;10

For the input file named H2in-a1.txt With the RNG unseeded, the current Skip List is shown below:

—infinity

110;

198;

270;

302; 302;

354;

503;

596;

603;

629; 629;

947;

+++infinity

—End of Skip List—

<h2>2.3           Classes and Functions</h2>

<h3>2.3.1          Classes</h3>

<strong>SkipList </strong>The <em>SkipList </em>class shall contain, at a minimum, the following methods.

<strong>insert </strong>The features and performance of the <em>insert </em>method is defined by the behavior described above.

<strong>promote </strong>The features and performance of the <em>promote </em>method is defined by the behavior described in the behavior of the insert commmand decribed above.

<strong>delete </strong>The features and performance of the <em>delete </em>method is defined by the behavior described above. <strong>search </strong>The features and performance of the <em>search </em>method is defined by the behavior described above.

<strong>printAll </strong>The <em>printAll </em>method prints the contents of the whole <em>skip list </em>in the format specified below.

Additional methods and properties will be required to successfully implement the methods specified above.

<strong>2.3.2    Functions complexityIndicator </strong>Prints to <strong>STDERR </strong>the following:

NID

A difficulty rating of difficult you found this assignment on a scale of 1.0 (easy-peasy) through 5.0 (knuckle busting degree of difficulty).

Duration, in hours, of the time you spent on this assignment.

Sample output:

EUSTIS_SYSTEM_PROMPT$java Hw02 H2in-a1.txt bs123456;3.141592653;10

<h1>3             Testing</h1>

Make sure to test your code on Eustis <strong><u>even if it works perfectly on your machine</u></strong>. If your code does not compile on Eustis you will receive a 0 for the assignment. There will be 10 input files and 10 output files provided for testing your code, they are respectively shown in Table 2 and in Table 3.

<table width="458">

 <tbody>

  <tr>

   <td width="102">Filename</td>

   <td width="356">Description</td>

  </tr>

  <tr>

   <td width="102">H2in-a1.txt</td>

   <td width="356">Inserts 10 integers, prints the <em>skip list</em></td>

  </tr>

  <tr>

   <td width="102">H2in-a2.txt</td>

   <td width="356">Inserts 25 integers, prints the <em>skip list</em></td>

  </tr>

  <tr>

   <td width="102">H2in-a3.txt</td>

   <td width="356">Inserts 50 integers, prints the <em>skip list</em></td>

  </tr>

  <tr>

   <td width="102">H2in-a4.txt</td>

   <td width="356">Inserts 100 integers, prints the <em>skip list</em></td>

  </tr>

  <tr>

   <td width="102">H2in-a5.txt</td>

   <td width="356">Inserts 27 integers, deletes 2 <strong>random </strong>numbers, prints the <em>skip list</em></td>

  </tr>

  <tr>

   <td width="102">H2in-a6.txt</td>

   <td width="356">Inserts 26 integers, searches for 1 <strong>random </strong>number, deletes 1 <strong>random </strong>number, prints the <em>skip list</em></td>

  </tr>

  <tr>

   <td width="102">H2in-a7.txt</td>

   <td width="356">Inserts 25 integers, searches for 2 <strong>random </strong>numbers, prints the <em>skip list</em></td>

  </tr>

  <tr>

   <td width="102">H2in-a8.txt</td>

   <td width="356">Inserts 798 integers, deletes 201 <strong>random </strong>numbers, prints the <em>skip list</em></td>

  </tr>

  <tr>

   <td width="102">H2in-a9.txt</td>

   <td width="356">Inserts 3957 integers, deletes 1043 <strong>random </strong>numbers, prints the <em>skip list</em></td>

  </tr>

  <tr>

   <td width="102">H2in-a10.txt</td>

   <td width="356">Inserts 4008 integers, deletes 993 <strong>random </strong>integers, prints the <em>skip list</em></td>

  </tr>

 </tbody>

</table>

Table 2: Input files

The expected output for these test cases will also be provided as defined in Table 3. To compare your output to the expected output you will first need to redirect <em>STDOUT </em>to a text file. Run your code with the following command (substitute the actual names of the input and output file appropriately):

java Hw02 <em>inputFile </em>&gt; output.txt

The run the following command (substitute the actual name of the expected output file): diff output.txt <em>expectedOutputFile</em>

<strong>Make sure that the </strong>Random Number Generator <strong>is NOT seeded with anything other than </strong>42<strong>. </strong>That is, do not use the <strong>r </strong>option when testing.

If there are any differences the relevant lines will be displayed (note that even a single extra space will cause a difference to be detected). If nothing is displayed, then congratulations – the outputs match! For each of the five (5) test cases, your code will need to output to <em>STDOUT </em>text that is identical to the corresponding <em>expectedOutputFile</em>. If your code crashes for a particular test case, you will not get credit for that case.

<h1>4             Submission – via WebCourses</h1>

The Java source file(s). Make sure that the <em>main </em>program is in Hw02.java.

Use reasonable and customary naming conventions for any classes you may create for this assignment.

<h1>5                  Sample output</h1>

EUSTIS_SYSTEM_PROMPT$java Hw02 H2in-a1.txt bs123456;3.141592653;10

For the input file named H2in-a1.txt With the RNG unseeded, the current Skip List is shown below:

—infinity

110;

198;

270;

302; 302;

354;

503;

596;

603;

629; 629;

947;

+++infinity

—End of Skip List—

<em>Note: This is based on an actual </em><em>skip list output using the inputs specified in the commands shown above.</em>

<strong>Note </strong>The <strong>bs123456;3.141592653;10 </strong>output shown above is the output from the <em>complexityIndicator </em>function to <strong>STDERR</strong>.

<table width="594">

 <tbody>

  <tr>

   <td width="352">Command</td>

   <td width="243">Validly formatted output files</td>

  </tr>

  <tr>

   <td width="352">java Hw02 in5.txt <em>&gt; </em>in5St.txt</td>

   <td width="243">in5Valid.txt</td>

  </tr>

  <tr>

   <td width="352">java Hw02 in5del1srch1.txt <em>&gt;</em>in5del1srch1St.txt</td>

   <td width="243">in5del1srch1Valid.txt</td>

  </tr>

  <tr>

   <td width="352">java Hw02 in5del2.txt <em>&gt;</em>in5del2St.txt</td>

   <td width="243">in5del2Valid.txt</td>

  </tr>

  <tr>

   <td width="352">java Hw02 in10.txt <em>&gt; </em>in10St.txt</td>

   <td width="243">in10Valid.txt</td>

  </tr>

  <tr>

   <td width="352">java Hw02 in100.txt <em>&gt; </em>in100St.txt</td>

   <td width="243">in100Valid.txt</td>

  </tr>

  <tr>

   <td width="352">java Hw02 in100m5000.txt <em>&gt; </em>in100m5000St.txt</td>

   <td width="243">in100m5000Valid.txt</td>

  </tr>

  <tr>

   <td width="352">java Hw02 in10k-m5000.txt <em>&gt; </em>in10k-m5000St.txt</td>

   <td width="243">in10k-m5000Valid.txt</td>

  </tr>

  <tr>

   <td width="352">java Hw02 in1m-m1000.txt <em>&gt; </em>in1m-m1000St.txt</td>

   <td width="243">in1m-m1000Valid.txt</td>

  </tr>

 </tbody>

</table>

Table 3: Commands with input files and corresponding

<a href="#_ftnref1" name="_ftn1">[1]</a> Quoted from William Pugh’s write up on <a href="https://en.wikipedia.org/wiki/Skip_list">Wikipedia.</a>