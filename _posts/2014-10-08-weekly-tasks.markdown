---
layout: post
title:  "Tutorials in Using HarvestAPI in PHP (Pt. 3)"
date:   2014-10-08 11:31:00
categories: jekyll update
---

On Wednesday October 8, 2014 I continued working on HarvestAPI with PHP. Used the endpoints Crop and Prices 
and did a search to show me some of the results in a table. <br/>

<h2> <b> Navigating Through Crops Using HarvestAPI </b> </h2> 
<br/>

<h3> <b> Going Through Crops Endpoint </b> </h3>
You can check out the crops endpoint at: <a href="http://harvestdata.herokuapp.com/crops/"> HarvestAPI Crops </a> <br/>

<h3> <b> Accessing The Crop Data Through a PHP Snippet </b> </h3> 
Now you can access the data with any platform of your choice, but for me I will be using PHP especially since
from the previous page I created a connection to HarvestAPI utilizing both PHP and cURL called `CallHarvestAPI.php`. 
You can see a view of the snippet below: 
<br/><br/>

{% highlight PHP %}
<?php
	include("CallHarvestAPI.php");

	/*---------------------------------------------------------------------------------------*/
	/*---------------------------------- Crop Details ---------------------------------------*/
	/*---------------------------------------------------------------------------------------*/
		
	$cropname = $_GET['crop_name'];

	// call crops resource to return string
	$crops = CallAPI('GET', 'harvestdata.herokuapp.com/crops/',
				array('search'=>$cropname, 'ordering'=>'-plant_date'));

	//convert JSON string to PHP variable (object)
	$crop_objects = json_decode($crops);
		
	$num_crops = $crop_objects -> count;
	$next_page_crop_url  = $crop_objects -> next;
		
	// getting the actual crops from results
	$crops_dem = $crop_objects -> results;
?>
	
<form action="crops.php" method="get">
	<fieldset>
		<legend> Search By Crop Name </legend>
		Crop Name <input type="text" name = "crop_name"/> <input type="submit"/>			
	</fieldset>
	
	</form>		
	<br />
	<br />
	<table>
		<tr>
			<td> Crop Name </td>
			<td> Estimated Volume </td>	
			<td> Area </td>
			<td> Plant Date </td>
			<td> Expiry Date </td>
		</tr>
			
<?php 
			
foreach($crops_dem as $crop)
{
	echo '<tr>
			<td>'.$crop -> crop_name.'</td>
			<td>'.$crop -> estimated_vol. '</td>
			<td>'.$crop -> area. '</td>
			<td>'.$crop -> plant_date. '</td>
			<td>'.$crop -> exp_date. '</td>
			</tr>';			
}				
?>
{% endhighlight %}

<br/><br/>
