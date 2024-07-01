# Lecture1


<html>
<head>
  <title>Relational database</title>
  <link rel=stylesheet type="text/css" href="../styl.css">
  <script language="JavaScript" src="../skrypty.js" type="text/javascript"></script>
</head>

<body>
<a name="poczatek"/>
<h2 align="center">Lecture 1</h2>

<h2 align="center"><i>Relational database and database management system</i></h2>

<hr><h3>Abstract</h3>

<p>In lecture 1 we explain the fundamental concepts of databases.
In particular we present <i>the relational data model</i>. Modern commercial
databases are based on this model.  We have also enclosed some information on <i>the
client-server architecture</i> which is used in database applications.  At the end of the lecture
you will find a brief summary of the history of databases.</p>

<p>None of the exercises for this lecture require using any software.</p>

<hr><h3><a name="database">Database</a></h3>

<p>Here are some general facts that drive the whole domain of databases.</p>

<ol>
<li><i>The data</i> is an asset of the company just like the others
	(employees, machines, stock).  The data must be <i>managed</i>
	just like the other
	assets.
<li><i>The information</i> is the data with semantics (defined by the meaning of the data
	in the company).
<li>The management of data is realized by <i>the information system</i>
	that caters for the need for information inside the company.
<li><i>The database</i> has become the standard means to structure the process
	of data management.
<li>The database is a part of the information system of the company.
</ol>

<h4><a name="w">Why is this lecture important and interesting?</a></h4>
 
<ul>
<li>Information is ubiquitous:
	<ul>
	<li>from simple services in web browsers
	<li>to scientific applications.
	</ul>
<li>There are more and more collections of data varying in the degree of
	complexity and size.
	<ul>
	<li>electronic libraries, multimedia databases, interactive video,
		the exploration of the human genome, space exploration (e.g. NASA).
	</ul>
<li>The development of a database requires expertise in many areas
	of information technology:
	<ul>
	<li>operating systems, information theory, artificial intelligence,
		programming languages, multimedia, software engineering.
	</ul>
<li>Database systems constitute one of the largest and most active 
parts of the market.
</ul>

<h4><a name="Aspekty">Information system</a></h4>

<p>Some aspects of an information system highlight its implementation nature:</p>

<ul>
<li><i>The database application</i> is considered, when we want to pay 
	closer attention
	to the software and to emphasize the remarkable role of the database.
<li><i>The computer system</i> is considered, when we want to pay closer attention
	to all computer-related artifacts, i.e. both hardware and software.
</ul>

<hr><h3><a name="rmd">Relational data model</a></h2>

<p>Relation data model was invented by Edgar Codd and presented for the first time
in a paper in 1970.  From the mathematical point o view <i>a database</i> is
a set of </i>relations</i>.   This is why we talk about <i>the relational data model</i>
and <i>relational databases</i>.  Mathematicians define a relation as a subset of the
Cartesian product of some sets.  A relation may be represented as
<a name="tabela-def"><i>a two-dimensional table</i></a> that consists of <i>rows</i> and <i>columns</i>.
We assume that:

<ol>
<li>The number of columns is fixed.
<li>Each column is assigned <i>a name</i> and <i>a domain</i>.
<li>There is exactly one atomic value at the intersection of a row and a column.
	This value belongs to the domain of this column.
<li>A row represents a single chunk of information, e.g. a person.
<li>We take no account of the order of rows (records) and columns (fields of records).
</ol>

<h4><a name="Tabela">Table <i>Teachers</i></a></h4>

<table border="1" align="center">
<tr><th>TeacherId	<th>FirstName	<th>LastName	<th>Title
<tr><td>2137		<td>Lech	<td>Banachowski	<td>Prof.
<tr><td>3245		<td>Krzysztof	<td>Stencel	<td>Dr.
<tr><td>8976		<td>John	<td>Smith	<td>Mr.
</table>

<h4><a name="Tabela2">Table <i>Lectures</i></a></h4>

<table border="1" align="center">
<tr><th>LectureName			<th>Code	<th>TeacherId
<tr><td>Databases			<td>DBA		<td>2137
<tr><td>Information systems		<td>INS		<td>3245
<tr><td>Internet technologies		<td>INT		<td>3245
<tr><td>Object-oriented programming	<td>OOP		<td>8976
<tr><td>Expert systems			<td>EXS		<td>2137
</table>


<p><table><tr><td class="przyk">
<p>Column <i>TeacherId</i> of table <i>Lectures</i> is specific, because:</p>

<ol>
<li>Its values do not describe properties of lectures.
<li>It represents <i>the relationship</i> between the lecture and
	a teacher, whose data is stored in a separate table.  In order to retrieve this
	data we have to use the identifier and find appropriate row in the related
	table.
<li>Therefore, it is important that this identifier uniquely determines the teacher.
	In the relational data model there is no other means of setting
	the identity of a row.
	You can do it by means of the stored values only.
</ol>
</td></tr></table>

<hr><h3><a name="Znaczenie">Primary key and unique keys</a></h3>

<ol>
<li>In every table there must be a unique identifier. We call it <i>the primary key</i>
	It is a subset (may be a singleton) of the columns of the table such that 
	the values in these columns uniquely identify the row.
<li><i>A unique key</i> (or <i>alternative key</i> or simply <i>key</i>) has the same
	property as the primary key.  However, there is only one primary key,
 	whereas
	the number of unique keys may be grater than one.
</ol>

<table><tr><td class="przyk">
<p>The primary key of the table <i>Lectures</i> is the column <i>Code</i>.  
	The column 
	<i>LectureName</i> is a unique key.</p>

<p>The primary key of the table <i>Teacher</i> is the column <i>TeacherId</i>.
	The column 
	<i>SecondName</i> need not be a key.</p>
</td></tr></table>

<p>Please answer the following simple question:</p>

<table><tr><td class="notec">
<a href="javascript:popUp('ok1.html',380,50)">How</a>
many primary keys may a table have?</td></tr></table> 

<hr><h3><a name="Klucze">Foreign key</a></h3>

<p><i>A foreign key</i> is the set of one or more columns whose values
are also the values of the primary key or a unique key of the related table
(it can be the same table).  The values of these columns are interpreted
as pointers to the rows of the related table.</p>
	

<table><tr><td class="przyk">
<p>Column <i>TeacherId</i> of table <i>Lectures</i>
is a foreign key that references column <i>TeacherId</i> of table <i>Teachers</i>.</p>

<p>For example number 2137 in the row of table <i>Lectures</i>
that describes lecture "Databases" is a reference to the row of table
<i>Teachers</i> that stores information on the teacher named "Banachowski".
This relationship reads:</p>

<p align="center"><i>Lecture "Databases" is taught by Lech Banachowski.</i></p>
</td></tr></table>

<p>Please answer the following simple question:</p>

<table><tr><td class="notec">
<a href="javascript:popUp('ok2.html',420,50)">How</a>
many foreign keys may a table have?</td></tr></table> 


<hr><h3><a name="NULL">Null = lack of value</a></h3>

<p>Domains of all columns are extended by the special value called <code>Null</code>.
The meaning of <code>Null</code> is the lack of values.  It could be:
<ul>
<li>temporary or
<li>permanent (<code>Null</code> is something else than the empty string or zero).
</ul>

All comparisons with <code>Null</code> yield <code>Null</code> as the result
(expression <code>Null=Null</code> also evaluates <code>Null</code>).
It concerns almost all operations that have <code>Null</code> as the argument
- their value is <code>Null</code>.</p>

<p>Therefore, <code>Null</code> is the third logical value besides
<code>True</code> and <code>False</code>.  Here are the truth tables for three major
logical connectives:</p>

<h4>Disjunction (<code>OR</code>)</h4>

<table border="1" align="center">
  <tr>
    <td align="left" bgcolor="#FFFFCC">
      <b>
      OR&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</b></td>
    <td align="left" bgcolor="#FFFFCC">
      <b>
      True&nbsp;&nbsp;&nbsp;</b></td>
    <td align="left" bgcolor="#FFFFCC">
      <b>
      False&nbsp;&nbsp;&nbsp;&nbsp;</b></td>
    <td align="left" bgcolor="#FFFFCC">
      <b>
      Null&nbsp;&nbsp;&nbsp;&nbsp;</b></td>
  </tr>
  <tr>
    <td align="left" bgcolor="#FFFFCC">
      <b>
      True</b></td>
    <td align="left">
      True</td>
    <td align="left">
      True</td>
    <td align="left">
      True</td>
  </tr>
  <tr>
    <td align="left" bgcolor="#FFFFCC">
      <b>
      False</b></td>
    <td align="left">
      True</td>
    <td align="left">
      False</td>
    <td align="left">
      Null</td>
  </tr>
  <tr>
    <td align="left" bgcolor="#FFFFCC">
      <b>
      Null</b></td>
    <td align="left">
      True</td>
    <td align="left">
      Null</td>
    <td align="left">
      Null</td>
  </tr>
</table>

<h4>Conjunction (<code>AND</code>)</h4>

<table border="1" align="center">
  <tr>
    <td align="left" bgcolor="#FFFFCC">
      <b>
      AND&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</b></td>
    <td align="left" bgcolor="#FFFFCC">
      <b>
      True&nbsp;&nbsp;&nbsp;</b></td>
    <td align="left" bgcolor="#FFFFCC">
      <b>
      False&nbsp;&nbsp;&nbsp;&nbsp;</b></td>
    <td align="left" bgcolor="#FFFFCC">
      <b>
      Null&nbsp;&nbsp;&nbsp;&nbsp;</b></td>
  </tr>
  <tr>
    <td align="left" bgcolor="#FFFFCC">
      <b>
      True</b></td>
    <td align="left">
      True</td>
    <td align="left">
      False</td>
    <td align="left">
      Null</td>
  </tr>
  <tr>
    <td align="left" bgcolor="#FFFFCC">
      <b>
      False</b></td>
    <td align="left">
      False</td>
    <td align="left">
      False</td>
    <td align="left">
      False</td>
  </tr>
  <tr>
    <td align="left" bgcolor="#FFFFCC">
      <b>
      Null</b></td>
    <td align="left">
      Null</td>
    <td align="left">
      False</td>
    <td align="left">
      Null</td>
  </tr>
</table>

<h4>Negation (<code>NOT</code>)</h4>

<table border="1" align="center">
  <tr>
    <td bgcolor="#FFFFCC">
      <b>
      NOT&nbsp;</b></td>
    <td bgcolor="#FFFFCC">
      <b>
      True&nbsp;</b></td>
    <td bgcolor="#FFFFCC">
      <b>
      False&nbsp;</b></td>
    <td bgcolor="#FFFFCC">
      <b>
      Null&nbsp;</b></td>
  </tr>
  <tr>
    <td>
      &nbsp;</td>
    <td>
      False</td>
    <td>
      True</td>
    <td>
      Null</td>
  </tr>
</table>

<p>It is time for a simple question:</p>

<table><tr><td class="notec"><a href="javascript:popUp('ok3.html',400,50)">Is</a>
it possible that a logical expression is true, when one if its arguments is <code>Null</code>?
</table> 

<h4>Predicates <code>Is Null</code> and <code>Is Not Null</code></h4>

<p>They allow recognizing null values. 

<blockquote>
<code>(X Is Null)</code> evaluates to <code>True</code>, when <code>X</code> is <code>Null</code><br>
<code>(X Is Null)</code> evaluates to <code>False</code>, when <code>X</code> is not <code>Null</code></blockquote>

However, be careful, because

<blockquote>
<code>(X = Null)</code> <b>always</b> evaluates to <code>Null</code>
(even for <code>X</code> being <code>Null</code>)
</blockquote>

Here is another simple question:</p>

<table><tr><td class="notec"><a href="javascript:popUp('ok4.html',350,50)">What</a>
is the logical value of expression <code>(Null=Null) Is Null</code>?
</table>

<hr><h3><a name="Wiezy">Integrity constraints</a></h3>

<p><i>Integrity constraints</i> are conditions that must 
be fulfilled by data in a database, e.g.</p>


<ul>
<li>a constraint for a single column:
	<pre>0 &lt; Age &lt; 140</pre>
<li>a constraint for several columns:
	<pre>birthDate &lt; hireDate</pre>
<li>the uniqueness (the primary keys, unique keys),
<li>NOT NULL constraint,
<li><a name="ref-cons"><i>the referential integrity</i></a>: each value of a foreign key is either 
	<code>Null</code> or occurs also in the appropriate column of the
	associated primary (or unique) key. 
<li>a more complex <i>business rule</i> that can be programmed in a more
	sophisticated language, e.g.
<pre>The sum of the salaries of all employees of a department
equals
the wage fund of this department.</pre>
</ul>

<p>Again a simple question:</p>

<table><tr><td class="notec">
<a href="javascript:popUp('ok5.html',350,130)">Which</a>
popular data model does not enforce referential integrity?
</table>

<hr><h3><a name="Perspektywy">View</a></h3>
 
<p><i>A view</i> is a virtual table to be used by the users, e.g.

<h4><a name="lect-teach">Lectures-Teachers</a></h4>

<table border="1" align="center">
<tr><th>LectureName			<th>Teacher
<tr><td>Databases			<td>Banachowski
<tr><td>Information systems		<td>Stencel
<tr><td>Internet technologies		<td>Stencel
<tr><td>Object-oriented programming	<td>Smith
<tr><td>Expert systems			<td>Banachowski
</table>

<p>The content of a usual view is calculated from the base tables at each usage.
It is not stored in the database. However, sometimes we need to save this
content in the database. Then we use this frozen image and do not recompute it
again and again. Such view is called <i>materialized</i>.</p>

<hr><h3><a name="indeks">Index</a></h3>

<p><i>An index</i> is an additional data structure that accelerates
access to the data in a table, when you search rows with particular values in 
a set of columns.  For example, the index built for column <i>LastName</i>
accelerates the search for the teacher with a given last name. The purpose of 
an index in a database is similar to that of the index in a book.</p>

<hr><h3><a name="Poziomy">Levels of a relational database</a></h3>

<p>The same data of a database may be viewed and processed in many different ways.
The point of view depends on the level of abstraction.  The basic levels of abstraction are:

<ol>
<li><i>The user level</i> consists of the views for users.
<li><i>The logical (conceptual) level</i> consists of views, tables and indexes.
<li><i>The physical level</i> consists of files with data and indexes.
</ol>

Views are defined on the logical level and used on the user level.
Indexes are defined on the logical level and used on the physical level.
Tables are defined on the logical level and used on the physical level and
the user level.</p>

<p>The user level is intended mainly for <i>the end users</i>.  The logical level is
used by <i>the system data administrator</i>, while <i>the database administrator</i>
(shortly <i>dba</i>) works with the physical level.  Of course, <i>the designer 
of the database</i> defines and works with all three levels.</p>

<p>Each level is somewhat independent.
For example, you can change the location 
of the data on the disk as well as the storage parameters without any impact 
on the logical structure of the tables.   Such a possibility is 
called <i>the physical data independence</i>.
You can also change tables without any change
of the applications, provided these are based on views and not directly tables. 
This feature is called <i>the logical data independence</i>.</p>

<p>Consider our sample database.  Its application can consist in displaying
the information on who delivers lectures, i.e. displaying the content of a view
<a href="#lect-teach">Lectures-Teachers</a>.  
In the future it may turn out that some lectures are given by more
than one teacher. The schema of the database with two tables
<i>Teachers</i> and <i>Lectures</i> is no longer sufficient.
A new associative table is required.  It will store the relationship 
between teachers and lectures. The definition of view 
<a href="#lect-teach">Lectures-Teachers</a> must be changed as well.
All these changes apply to the logical level of the database. The application
itself is based on this view and thus it need not be changed.  It is an
example of the meaning of the logical data independence.</p>

<p>The physical data independence becomes important, when the disk is already full
and we have to buy a new one. New rows will be stored on the new disk, but
neither the schemata of the tables nor the applications have to be changed.</p>

<hr><h3><a name="katalog">Catalog</a></h3>

<p><i>The catalog</i> (or <i>data dictionary</i> or <i>metadata</i>) is the 
collection of tables and views that describe the schema of the database.
In other words, the catalog contains definitions of all the objects
of all the three levels of the database.  The name and the data type of a column
are examples of metadata.</p>

<p>It is important to use the relational data model for the catalog.
This ensures that 
the metadata are stored and processed the same way as the data.</p>


<hr><h3><a name="Arch">Client-server architecture</a></h3>

<p>Database applications usually consists of at least two parts:</p>

<dl>
<dt><i>the client side</i>
<dd>that operates on the user's workstation,
<dt><i>the server side</i>
<dd>that operates on the computer that runs the database server, i.e. the
	database itself and the database management system (DBMS). 
</dl>

The functions performed at the server side are:

<ol>
<li>storing data and facilitating access to it,
<li>executing statements of the database language
	(usually it is SQL that will be presented during lecture 9),
<li>enforcing data integrity,
<li>managing the resources of the database, e.g. the users' accounts.
</ol>

The functions performed at the client side are:

<ol>
<li>interacting with the user (running the user interface),
<li>explaining the state of the computation to the user (it includes also
	errors and exceptional events),
<li>accepting users' queries and then executing them or 
	sending them to the server as SQL statements. 
</ol>

<hr><h3><a name="Historia">History of databases</a></h3>

<dl>
<dt>1951
<dd>Univac presented <i>the magnetic tape</i> as a means to store data.
	(Before that punched cards were used).
	<p align="center"><img border="0" src="images/univac.jpg"></p>
<dt>1956
<dd>IBM introduced <i>the magnetic hard drive</i>. 
<dt>1961
<dd>Integrated Data Store IDS (<i>Charles Bachman</i>, General Electric) was
	the first DBMS. It was the rise of <i>the network data model</i>.
<dt>1965-70
<dd>Information Management System IMS (IBM) - <i>the hierarchical data model</i>.
<dt>1970
<dd><i>Edgar Codd (1924-2003)</i>, IBM &#8211, <i>the relational data model</i>.
 	<p align="center"><img border="0" src="images/Codd.jpg"></p>
<dt>1971
<dd>CODASYL, the standard for the network data model.
<dt>1976
<dd>Peter Chen - <i>the entity-relationship model</i> (ERD, ERM).
	There is no standard for this model so far (in 2004).
<dt>The beginning of the seventies
<dd>People at IBM research lab in San Jose develop languge <i>Sequel</i>.
	It was the prototype of SQL.  You can still meet "old" people who pronounce
	SQL as "Sequel".  Now you know why they do it.
<dt>1973
<dd>The first relational database management system (<i>System R</i> developed by IBM).
<dt>1979
<dd>Relational Software (later rebranded to Oracle) marketed the first commercial
	version of a relational database management system.
<dt>1987
<dd>The first standard of SQL (ISO).
	<ul>
	<li>Next versions of standard SQL (by ANSI/ISO): 1989, 1992 SQL2, 1999 SQL3
		(the object-relational model).
	<li>SQL4 is developed.
	</ul>
<dt>The eighties
<dd>Reserch on deductive and object-oriented databases.
<dt>1997 
<dd>The standard for object-oriented databases: ODMG 2.0.
<dt>Since the nineties till now
<dd>Databases have been extended by <i>new aspects</i> like
	multi-tier architectures,
	distribution,
	integration,
	parallel computation,
	Internet,
	data warehouses,
	OLAP,
	multimedia,
	databases of documents (also XML),
	GIS (Geographical Information Systems), 
	ERP (Enterprise Resource Planning),
	MRP (Management Resource Planning) - packets like SAP,
	Baan, Oracle, PeopleSoft, Siebel, CRM (Customer Relationship Management).
</dl>

<hr><h3><a name="Podsumowanie">Summary</a></h3>

<p>During this lecture we explained the fundamental notions that apply to databases.
We also emphasized the importance of databases for information systems. In particular,
we presented the primary data model of modern databases. We call it <i>the relational
data model</i>.  We described the following concepts of this model:
<i>table</i>, <i>key</i>, <i>primary key</i>, <i>foreign key</i>, <i>view</i>,
<i>pseudo-value Null</i> and <i>integrity constraints</i>.</p>

<hr><h3><a name="Slownik">Dictionary</a></h3>

<dl>

<dt><a href="#Klucze">foreign key</a>
<dd>A set of one or more columns whose values are also values of the 
	primary key or a unique key of the related table (it can be the same table). 
	The values of these columns are interpreted as pointers to the rows 
	of the related table.

<dt><a href="#Wiezy">integrity constraint</a>
<dd>A correctness condition for the data in a database.

<dt><a href="#Znaczenie">key</a>
<dd>A subset (may be a singleton) of the columns of a table such that the values 
	in these columns uniquely identify the row of this table. 

<dt><a href="#NULL">Null</a> 
<dd>The pseudo-value which means that the data is missing.

<dt><a href="#Znaczenie">primary key</a>
<dd>The distinguished key which is used to identify objects.

<dt><a href="#ref-cons">referential integrity constraint</a>
<dd>An integrity constraint which states that 
	each value of a foreign key is either <code>Null</code> or occurs also
	in the apropriate column of the associated primary (or unique) key. 

<dt><a href="#tabela-def">table</a>
<dd>A two-dimensional structure which consists of <i>rows</i> and <i>columns</i>. 
	At the intersection of a row and a column there is only one atomic data item.
	A row stores a record of data on an object (e.g. a person or a company)
	or a relationship between objects. Each column contains a set of atomic data items
	which describe one of the attributes of an object (e.g. the name of the company
	or the last name of a person).

<dt><a href="#Znaczenie">unique key</a>
<dd>A key that is not primary.

<dt><a href="#Perspektywy">view</a>
<dd>A virtual table created for users.  It is defined on the logical level and used on the
	user level. If it is physically saved in the form of
	a relational table,
	we call it <i>a materialized view</i>.

</dl>

<hr><h3><a name="Zadania">Exercises</a></h3>

<ol>
<li>Give an example of two tables connected with the relationship <i>primary key-foreign key</i>.
	Define their primary keys. Do they have unique (alternative) keys?
	Define at least one foreign key. Draw both tables on paper and enter
	some rows into them.  Remember not to break the referential integrity.
<li>Reflect on the meaning of data and information in your life.
	Do you use any systems to store your data?
	Can you call these systems databases?
</ol>

<hr><i><font size="1">Page prepared in Polish by Lech Banachowski and
translated into English by Krzysztof Stencel.</font></i>

</body></html>
