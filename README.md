Download Link: https://assignmentchef.com/product/solved-csci1200-data-structures-homework-9-miniblast-hash
<br>
[pdf-embedder url="https://assignmentchef.com/wp-content/uploads/2022/12/file-11.pdf" title="file (11)"]

BLAST (<strong>B</strong>asic <strong>L</strong>ocal <strong>A</strong>lignment <strong>S</strong>earch <strong>T</strong>ool) is an algorithm for fast, efficient searching of databases of proteins, DNA, and RNA sequences. A BLAST search allows a researcher to compare a query sequence against a library of sequences. For example, after sequencing a gene from a newly discovered bacteria, BLAST can be used to determine if the gene is similar to any genes in known bacteria. You can read more about BLAST at <a href="https://en.wikipedia.org/wiki/BLAST">https://en.wikipedia.org/wiki/BLAST</a> or try it out at <a href="https://blast.ncbi.nlm.nih.gov/Blast.cgi">http://blast.ncbi.nlm.nih. </a><a href="https://blast.ncbi.nlm.nih.gov/Blast.cgi">gov/Blast.cgi</a><a href="https://blast.ncbi.nlm.nih.gov/Blast.cgi">.</a>

<em>Please carefully read the entire assignment before beginning your implementation.</em>

In this homework assignment, we create an extremely simplified version of BLAST. Our version works in a manner somewhat similar to BLAST, but the BLAST algorithm is sophisticated and BLAST software is highly optimized. BLAST is used to regularly search Genbank, a repository of sequence data containing over 1 trillion bases (letters) of sequence data. Online searches are typically returned in less than a minute. We won’t try anything quite so ambitious. Our version of BLAST, MiniBLAST, will search small genome files with query strings in a DNA alphabet (A,C,G,T).

The genome files that we will search will consist of a number of lines, each line containing letters from the DNA alphabet. Here are the first few lines of the <em>genome </em><em>small.txt </em>file:

$ head genome_small.txt

TAATGACCTAAATAATCTAAACAAAAGGAAGAGAGATAGTCCGGATTACC

TGGGACATGGAAAACCCTCCTTTCTCTCATCAGCTTCCCACCCCACCTCT

GCCCAGCGCTAATCATGATTTAATAGCCTTCCTTAATCACTTACTCTGTT

TGCTGCTTCATCTAAAAACTTAAGATGCTCTGGGTTAGATCACAGTCTAA

CTCATCACAAATGGATAGAACGACCTGGTAGTTTTCCAGATTTCCATTGT

CCAAACTAATCAGCCAACACACTCAATGATGCACATTATTTTCCACGTAT

ATGGCCTTAGAGATGGGACTAAAAGTCCCGACTGTACTGAGGATGTTTGA

CAGGTTTTGCCATTCTAACTGCTAGTGCTGTGTAATGTGGCTAGGAAGAA

GCAAGGAACAGAGAGATACAGATATGATTTCCTGGGACCAGCTATAGGAG

AGATTCTTCAATTACATCATCTTTGCTCATCCCAAACACCTTGACAAGTA

The genome data above is a small region from human chromosome 18.

The queries will be also strings from the DNA alphabet. A typical query could look like:

CTCATCACAAATGGATAGAACGACCTGGTA

This query can be located at the start of the 5th line.

The strategy that we will employ is to index the genome file with a series of <em>k-mers</em>. A <em>k-mer </em>is a sequence of <em>k </em>letters from the DNA alphabet, where <em>k </em>is an integer. A given <em>k-mer </em>may appear many times within the genome.

We index the genome by building a <strong>hash table </strong>with the <em>k-mers </em>as the keys. The hash table is to be implemented with an array or a vector at the top level. A <em>hash function </em>will map the <em>k-mer </em>to a position in the table. You will chose an appropriate structure to store the <em>kmers </em>and genomic locations of the <em>k-mers</em>, i.e. the positions where they are found in the genomic sequence. You build the hash table by iterating through the genome sequence with a series of overlapping windows of length <em>k</em>, calculating the the index into the hash table using the hash function. Store the <em>kmer </em>and its genomic location in the table. When iterating through the genome sequence, the first <em>k-mer </em>is the genome sequence from 0 to k-1; the second is the sequence from 1 to k, etc.

When searching a biological sequence database, it’s often the case that we do not find an exact match to a query string. MiniBLAST will process queries of varying lengths and allow for mismatches between the genome and query string. To search the genome, MiniBLAST uses the first <em>k </em>letters of the query string as a seed. It is important that searching the database for the initial seed be efficient. Thus, the choice of hash function and table implementation is important. If the seed can be found in the table, the program should try to extend the match by adding letters from the indexed genomic position until the full query is matched or the allowed number of mismatches is exceeded. For simplicity we require that the seed be an exact match. The mismatches may occur anywhere after the seed in the match string.
<h1>Choice of Hash Function and Table Implementation</h1>
The choice of the hash function is up to you. A good hash function should be fast, O(1) computation, and provide a random, uniform distribution of keys throughout the table. You may use one of the hash functions mentioned in lecture, one found on the internet, or one of your own devising. If you choose to download a hash function from the internet, you must provide the URL in your README and include the source code with your submission. If the downloaded file requires a copyright notice, you MUST include that notice. Be sure to observe any copyright restrictions on the use of the code. In your README file, describe your hash function and table implementation.

A typical <em>k-mer </em>will be found in several location in the genome. Your hash table implementation should enable efficient retreival of the multiple locations where the <em>k-mer </em>is found.

To store the <em>k-mers </em>and their genomic positions in the hash table, once the table index of the <em>kmer </em>key has been found, you may use any of the data structures that we have covered so far in class. To handle collisions, use one of the open addressing methods described in lecture (linear probing, quadratic probing, or secondary hashing). Linear probing is the simplest of these three methods. You may not use <em>std::hash</em>, <em>std::unordered map</em>, <em>std::unordered </em><em>set</em>, <em>std::map </em>or similar STL functions/containers.

When implementing the hash table, set the initial size of the table. As you enter data in the table, calculate the occupancy ratio:

When the <em>occupancy &gt;</em>than some fixed level, double the size of the table and rehash the data. Describe your re-sizing method in the hash table section of the README file.
<h1>Input/Output &amp; Basic Functionality</h1>
The program should read a series of commands from std::cin (STDIN) and write responses to std::cout (STDOUT). Sample input and output files have been provided. You can redirect the input and output to your program using the instructions in the section <strong>Redirecting Input &amp; Output </strong>found at <a href="http://www.cs.rpi.edu/academics/courses/spring17/ds/other_information.php">http: </a><a href="http://www.cs.rpi.edu/academics/courses/spring17/ds/other_information.php">//www.cs.rpi.edu/academics/courses/spring17/ds/other_information.php</a>

Your program should accept the following commands:
<ul>
 	<li><em>genome filename </em>– Read a genome sequence from <em>filename</em>. The genome file consists of lines DNA characters.</li>
 	<li><em>table size N </em>– this is an optional command. <em>N </em>is an integer. It is the initial hash table size. If it does not appear in the command file, the initial table size should be set to 100.</li>
 	<li><em>occupancy f </em>– this is an optional command. <em>f </em>is a float. When the occupancy goes above this level, the table should be resized. If it does not appear in the command file, the initial level should be set to 0.5.</li>
 	<li><em>kmer k </em>– <em>k </em>is an integer. The genome should be indexed with <em>kmers </em>of length <em>k</em>.</li>
 	<li><em>query m query </em><em>string </em>– Search the genome for a match to <em>query </em><em>string </em>allowing for <em>m </em></li>
 	<li><em>quit </em>– Exit the program.</li>
</ul>
Ignore blank lines in the file.

Here is some sample input, showing typical commands:

genome genome_small.txt table_size 100 occupancy 0.5 kmer 10 query 2 TATTACTGCCATTTTGCAGATAAGAAATCAGAAGCTC query 2 TTGACCTTTGGTTAACCCCTCCCTTGAAGGTGAAGCTTGTAAA query 2 AAACACACTGTTTCTAATTCAGGAGGTCTGAGAAGGGA query 2 TCTTGTACTTATTCTCCAATTCAGTCACAGGCCTTGTGGGCTACCCTTCA query 5 TTTTTTTTTTTTTTTCTTTTTT quit

You may assume that the commands will appear in the input files in the order shown above.

For output, the program will report the query, and if matches are found, the genome position (positions start at 0) of the match, the number of mismatches between the genome and the query string, and the genome sequence matching the query. If a match can’t be found, the program will report “No Match”.

The corresponding output to the input above should be:

Query: TATTACTGCCATTTTGCAGATAAGAAATCAGAAGCTC

504 0 TATTACTGCCATTTTGCAGATAAGAAATCAGAAGCTC

Query: TTGACCTTTGGTTAACCCCTCCCTTGAAGGTGAAGCTTGTAAA

5002 2 TTGACCTTTGGTTAACCAATCCCTTGAAGGTGAAGCTTGTAAA

Query: AAACACACTGTTTCTAATTCAGGAGGTCTGAGAAGGGA

4372 0 AAACACACTGTTTCTAATTCAGGAGGTCTGAGAAGGGA

Query: TCTTGTACTTATTCTCCAATTCAGTCACAGGCCTTGTGGGCTACCCTTCA

No Match

Query: TTTTTTTTTTTTTTTCTTTTTT
<ul>
 	<li>0 TTTTTTTTTTTTTTTCTTTTTT</li>
 	<li>3 TTTTTTTTTTTTTTCTTTTTTG</li>
 	<li>4 TTTTTTTTTTTTTCTTTTTTGA</li>
 	<li>5 TTTTTTTTTTTTCTTTTTTGAG</li>
</ul>
You are not explicitly required to create any new classes when completing this assignment, but please do so as it will improve your program design. We expect you to use const and pass by reference/alias as appropriate throughout your assignment.
<h1>Order Notation</h1>
In your README.txt file, report the time and space complexity (order) of your implementation for building the index for a genome of length <strong>L</strong>. Does the <em>k-mer </em>size, <strong>k</strong>, and the average number of locations, <strong>p</strong>, where the key is found affect your answer? What is the order time notation for matching a query of length <strong>q </strong>in a genome of length <strong>L </strong>when the key size is <strong>k </strong>and the key is found at <strong>p </strong>different genomic positions?
<h1>Extra Credit</h1>
Add a new command to implement the database using one of the other data structures that we have covered so far in the course: vectors, lists, arrays etc. Compare the performance your alternative method to the homework method by making a table of run times for each of the genomes and query sets provided with the homework and compare the times to build the index and the times to process the queries. Document any new commands you have added in your README file.