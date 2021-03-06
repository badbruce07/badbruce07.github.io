---
layout: post
title:  "Tutorials in Using HarvestAPI with PHP (Pt. 3)"
date:   2014-10-09 11:31:00
categories: jekyll update
---

On Thursday October 9, 2014 I continued working on HarvestAPI with PHP. Used the endpoints Farmers and Farm 
and did a search to show me some of the results in a table. <br/>

<h2> <b> Navigating Through Farmers and Farm Using HarvestAPI </b> </h2> 
<br/>

<h3> <b> Going Through Farmers Endpoint </b> </h3>
You can check out the crops endpoint at: <a href="http://harvestdata.herokuapp.com/farmers/"> HarvestAPI Farms </a>

<h3> <b> Accessing The Farmers Data Through a PHP Snippet </b> </h3> 
Now you can access the data with any platform of your choice, but for me I will be using PHP especially since
from the previous page I created a connection to HarvestAPI utilizing both PHP and cURL called `CallHarvestAPI.php`. 
You can see a view of the snippet below: 
<br/><br/>

{% highlight PHP %}
<?php
	include("CallHarvestAPI.php");
		
	/*---------------------------------------------------------------------------------------*/
	/*---------------------------------- Farmer Details -------------------------------------*/
	/*---------------------------------------------------------------------------------------*/
	$first_name = $_GET['first_name'];

	//call farmers resource to return string
	$farmers = CallAPI('GET', 'harvestdata.herokuapp.com/farmers/', 
					array('search'=>$first_name, 'ordering'=>'last_name'));
		
	//convert JSON string to PHP variable (object)
	$farmer_objects = json_decode($farmers);

	$num_farmers = $farmer_objects->count;
	$next_page_url  = $farmer_objects->next;
		
	//now get the actual farmers from results
	$fama_dem = $farmer_objects->results;		
?>
		
<form action="farmers.php" method="get">
	<fieldset>
		<legend> Search By Farmer First Name: </legend>	
		Farmer First Name: <input type="text" name = "first_name"/> <input type="submit"/>		
	</fieldset>
</form>
<br />
<br />	
<table>
	<tr>
		<td> Farmer ID </td>	
		<td> First Name </td>
		<td> Last Name </td>
		<td> Parish </td>
		<td> Verified Status </td>			
	</tr>			
			
<?php
	foreach ($fama_dem as $fama) {
		echo '<tr>
					<td>'.$fama -> farmer_id.'</td>
					<td>'.$fama -> first_name. '</td>
					<td>'.$fama -> last_name. '</td>
					<td>'.$fama -> res_parish. '</td>
					<td>'.$fama -> verified_status. '</td>
				</tr>';
	}
?>
</table>
{% endhighlight %}
<br/><br/>

From the above snippet called `Farmers.php`, in line 2, I used an include function which calls the `CallHarvestAPI.php` snippet. 
In line 7 we created a variable name called <b> $first_name </b> which defines `$_GET['first_name']`. The variable `first_name` 
is in fact a field in farmers endpoint and is seen again in line 26 in our form. The aim is to search for a parish to display a 
list with the fields in the table. 
<br/>
In lines 10 a variable called $farmers and it is equivalent to CallAPI function that has 3 parameters. If you recall the CallAPI 
function that was in CallHarvestAPI.php the parameters include:
<ul>
	<li> $method = 'GET' </li>
	<li> $url = 'harvestdata.herokuapp.com/farmers/'</li>
	<li> $data = array('search'=>$first_name, 'ordering'=>'last_name') </li>
</ul>
<br/>
NB. For the $data variable, you can use any variable name such as `first_name`, `last_name`, `alias`, `res_parish`, `agri_activity`.
Farmers endpoint consists of field names such as `{"url", "farmer_id", "farmer_id", "first_name", "last_name", "alias", 
"res_address", "res_parish", "tel_number", "cell_number", "verified_status", "dob", "agri_activity", "owner"}`. Also, the ordering 
is done by the last name in ascending order.

<ul>
	<li> 
		In line 14, json_decode is used to decode a JSON string and then it becomes a PHP variable  <b>$farmer_objects</b>. 
	</li>
	<li> 
		In line 16, <b>$num_farmers</b> keeps a count of the number of farmers. 
	</li>
	<li> 
		In line 20, <b> $fama_dem </b> gets the farmers from results.	
	</li>
	<li>
		In lines 23-28, a form was created and a navigation was done by First Name. Of course the name must match 
		<b><u>first_name</u></b>, which is the value we are trying to get to print the rest of details of our choice. 
	</li>
</ul>
<br/>
Tables are created so that the results can be seen there and we have a foreach() loop to print the fields of our choice.<br />
Look at the table below: <br/>

![My helpful screenshot]({{ site.url }}/assets/screenshot_farmers.png)
<br/><br/>
As shown above the foreach() loop in line 41 takes care of each row that has details regarding the first name (take a look at 
the URL locator and you will see `first_name=Clover`)
<br/><br/><br/>

<h3> <b> Going Through Farm Endpoint </b> </h3>
You can check out the crops endpoint at: <a href="http://harvestdata.herokuapp.com/farms/"> HarvestAPI Farms </a> <br/>

<h3> <b> Accessing The Farm Data Through a PHP Snippet </b> </h3>
Now you can access the data with any platform of your choice, but for me I will be using PHP especially since from the previous page
I created a connection to HarvestAPI utilizing both PHP and cURL called CallHarvestAPI.php. You can see a view of the snippet below:
<br/><br/>

{% highlight PHP %}
<?php
	include("CallHarvestAPI.php");

	/*---------------------------------------------------------------------*/
	/*--------------------------- Farm Details ----------------------------*/
	/*---------------------------------------------------------------------*/
		
	$parish = $_GET['parish'];
		
	// call farms resource to return string
	$farms = CallAPI('GET', 'harvestdata.herokuapp.com/farms/', 
				array('search'=> $parish, 'ordering'=> 'extension'));

	//convert JSON string to PHP variable (object)
	$farm_objects = json_decode($farms);

	$num_farms = $farm_objects -> count;
	$next_page_farm_url = $farm_objects -> next;

	//getting the actual prices from results
	$farms_dem = $farm_objects -> results;
?>

<form action="farms.php" method="get">
	<fieldset>
		<legend> Search By Parish: </legend>	
		Parish Name: <input type="text" name = "parish"/> <input type="submit"/>		
	</fieldset>
</form>
<br />
<br />
<table>
	<tr>
		<td> Farm Address </td>
		<td> Farm ID </td>	
		<td> Parish </td>
		<td> District </td>
		<td> Extension </td>
	</tr>

<?php
foreach($farms_dem as $farm)
{
	echo '<tr>
		<td>'.$farm -> farm_address.'</td>
		<td>'.$farm -> farm_id. '</td>
		<td>'.$farm -> parish. '</td>
		<td>'.$farm -> district. '</td>
		<td>'.$farm -> extension. '</td>
	</tr>';	
}
?>
</table>

{% endhighlight %}

From the above snippet called `Farms.php`, in line 2, I used an include function which calls back the `CallHarvestAPI.php` snippet.
In line 7 we created a variable name called <b> $parish </b> which defines `$_GET['parish']`. The variable `parish` is in fact 
a field in farms endpoint and is seen again in line 26 in our form. The aim is to search for a parish to display a list with the 
fields in the table.
<br/>
In lines 10 a variable called $farms and it is equivalent to CallAPI function that has 3 parameters. 
If you recall the CallAPI function that was in CallHarvestAPI.php the parameters include:
<ul>
	<li> $method = 'GET' </li>
	<li> $url = 'harvestdata.herokuapp.com/farms/'</li>
	<li> $data = array('search'=>$parish, 'ordering'=>'-extension') </li>
</ul>
<br/>
NB. For the <b>$data</b> variable, you can use any variable name such as `parish`, `farm_address`, `farm_id`, `extension` and 
`farm_size`. Farms endpoint consists of field names such as `{"farm_address", "farm_id", "parish", "district", "extension", 
"farm_size", "lat", "long", "farmer"}`. Also, the ordering is done by extension in descending order since there is a (-) 
before the term extension.

<ul>
	<li> In line 14, json_decode is used to decode a JSON string and then it becomes a PHP variable <b> $farm_objects </b>. </li>
	<li> In line 16, $num_farms keeps a count of the number of crops. </li>
	<li> In line 20, $farms_dem gets the farms from results. </li>
	<li> In lines 23-28, a form was created and a navigation was done by Parish. Of course the name must match 
	     <b><u>parish</u></b>, which is the value we are trying to get to print the rest of details of our choice. 
	</li>
</ul>

Tables are created so that the results can be seen there and we have a foreach() loop to print the fields of our choice.<br />
Look at the table below: <br/>
![My helpful screenshot]({{ site.url }}/assets/screenshot_farms.png)
<br/><br/>

As shown above the foreach() loop in line 41 takes care of each row that has details regarding the parish name 
(take a look at the URL locator and you will see `parish=Trelawny`)