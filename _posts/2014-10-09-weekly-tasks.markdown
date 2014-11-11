---
layout: post
title:  "Tutorials in Using HarvestAPI in PHP (Pt. 3)"
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