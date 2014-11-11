---
layout: post
title:  "Tutorials in Using HarvestAPI in PHP (Pt. 2)"
date:   2014-10-08 11:31:00
categories: jekyll update
---

On Wednesday October 8, 2014 I continued working on HarvestAPI with PHP. Used the endpoints Crop and Prices 
and did a search to show me some of the results in a table. <br/>

<h2> <b> Navigating Through Crops and Prices Using HarvestAPI </b> </h2> 
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
</table>
{% endhighlight %}

<br/><br/>
From the above snippet called `Crops.php`, in line 11, we used an include function which calls back the `CallHarvestAPI.php` 
snippet. On line 8 we created a variable name  called <b> $cropname </b> which defines `$_GET['crop_name']`. The variable 
`crop_name` is in fact a field in crops endpoint and is seen again in line 27 in our form. The aim is to search for a crop name 
to display a list with the fields in the table. <br/>
In lines 11-12 a variable called <b>$crops</b> and it is equivalent to CallAPI function that has 3 parameters. 
If you recall the CallAPI function that was in CallHarvestAPI.php the parameters include:
<ul>
	<li> $method = 'GET' </li>
	<li> $url = 'harvestdata.herokuapp.com/crops/'</li>
	<li> $data = array('search'=>$cropname, 'ordering'=>'-plant_date') </li>
</ul>
<br/>
NB. For the <b> $data </b> variable, you can use any variable name such as `common_name`, `farm`, `farm_id`, `parish`.	<br/>
`Crops Endpoint` consists of field names such as `{"crop_name", "common_name", "estimated_vol", "variety, "plant_date", "count",
"area", "status", "exp_date", "farm"}`. Also, the ordering is done by plant_date in descending order since there is a (-) before 
the term `plant_date`.

<ul>
	<li>
		In line 14, <b> <u>json_decode</u> </b> is used to decode a JSON string and then it becomes a PHP variable 
		<b> $crop_objects. </b>
	</li>
	<li>
		In line 16, <b> $num_crops </b> keeps a count of the number of crops.				  	
	</li>
				  	
	<li>
		In line 20, <b> $crops_dem </b> gets the crops from results.				  	
	</li>
	<li>
		In lines 23-29, a form was created and a navigation was done by Crop Name. Of course the name must match 
		<b><u>crop_name</u></b>, which is the value we are trying to get to print the rest of details of our choice.
	</li>
</ul>
<br/>
Tables are created so that the results can be seen there and we have a foreach() loop to print the fields of our choice. <br/>
Look at the table below: <br/>
![My helpful screenshot]({{ site.url }}/assets/screenshot_crops.png)
<br /> <br />
						
As shown above the foreach() loop in line 41 takes care of each row that has details regarding the crop name 
(take a look at the URL locator and you will see `crop_name=Potato`)
<br/><br/><br/>

<h2> <b> Navigating Through Prices Using HarvestAPI </b> </h2> 
<br/>

<h3> <b> Going Through Prices Endpoint </b> </h3>
You can check out the crops endpoint at: <a href="http://harvestdata.herokuapp.com/prices/"> HarvestAPI Prices </a> <br/>

<h3> <b> Accessing The Prices Data Through a PHP Snippet </b> </h3>
Now you can access the data with any platform of your choice, but for me I will be using PHP especially since
rom the previous page I created a connection to HarvestAPI utilizing both PHP and cURL called CallHarvestAPI.php. 
You can see a view of the snippet below: 
<br/><br/>

{% highlight PHP %}

<?php
	include("CallHarvestAPI.php");

	/*---------------------------------------------------------------------------------------*/
	/*-------------------------------- Livestock Details ------------------------------------*/
	/*---------------------------------------------------------------------------------------*/
		
	$commodity = $_GET['commodity'];

	// call price resource to return string
	$prices = CallAPI('GET', 'harvestdata.herokuapp.com/prices/',
				array('search'=> $commodity, 'ordering'=>'price'));
					
	//convert JSON string to PHP variable (object)
	$price_objects = json_decode($prices);
			
	$num_prices = $price_objects -> count;
	$next_page_price_url = $price_objects -> next;
			
	//getting the actual prices from results
	$prices_dem = $price_objects -> results;
?>
	
<form action="prices.php" method="get">
	<fieldset>
		<legend> Search By Commodity Name </legend>
		Commodity: <input type="text" name = "commodity"/> <input type="submit"/>		
	</fieldset>
</form>
<br />
<br />
<table>
	<tr>
		<td> Price </td>
		<td> Commodity </td>	
		<td> Parish </td>
		<td> Batch Date </td>
		<td> Published On </td>
	</tr>
			
<?php 
			
foreach($prices_dem as $price)
{	
	echo '<tr>
				<td>'.$price -> price.'</td>
				<td>'.$price -> commodity. '</td>
				<td>'.$price -> parish. '</td>
				<td>'.$price -> batch_date. '</td>
				<td>'.$price -> published_on. '</td>
			</tr>';
}
			
/*---------------------------/////////////////////////////--------------------------------*/
/*------------------------------- End of Price Details -----------------------------------*/
/*--------------------------//////////////////////////////--------------------------------*/			
			
?>
</table>

{% endhighlight %}

From the above snippet called `Prices.php`, in line 2, we used an include function which calls back the `CallHarvestAPI.php` 
snippet. On line 8 we created a variable name called <b> $commodity </b> which defines `$_GET['commodity']`. The variable 
`commodity` is in fact a field in prices endpoint and is seen again in line 27 in our form. The aim is to search for a commodity 
name to display a list with the fields in the table.
<br/>
In lines 11 a variable called <b> $prices </b> and it is equivalent to CallAPI function 
that has 3 parameters. If you recall the CallAPI function that was in CallHarvestAPI.php the parameters include:
<br/>
<ul>
	<li> $method = 'GET' </li>
	<li> $url = 'harvestdata.herokuapp.com/prices/'</li>
	<li> $data = array('search'=>$commodity, 'ordering'=>'price') </li>
</ul>
<br/>
NB. For the <b>$data</b> variable, you can search by `commodity`, `crop_code`, `price_point`, `extension` and `parish`.	
Livestock Endpoint consists of field names such as `{"price", "public", "price_point", "parish", "commodity", "crop_code", 
"units", "variety", "batch_date", "published_on", "extension"}`. Also, the ordering is done by price in ascending order.

<ul>
	<li>In line 14, json_decode is used to decode a JSON string and then it becomes a PHP variable <b> $price_objects </b>.	</li>
	<li> In line 16, <b> $num_prices </b> keeps a count of the number of livestock. </li>
	<li> In line 20, <b> $prices_dem </b> gets the livestock from results. </li>
	<li> In lines 23-29, a form was created and a navigation was done by Commodity. Of course the name must match 
		  <b><u>commodity</u></b>, which is the value we are trying to get to print the rest of details of our choice. </li>
</ul>		
Tables are created so that the results can be seen there and we have a foreach() loop to print the fields of our choice.
Look at the table below: <br/>	
![My helpful screenshot]({{ site.url }}/assets/screenshot_prices.png)
<br/><br/>

As shown above the foreach() loop in line 41 takes care of each row that has details regarding the livestock name (take a 
look at the URL locator and you will see `commodity=Dasheen`)	