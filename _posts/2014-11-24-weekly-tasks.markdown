---
layout: post
title:  "Merging HarvestAPI demo To The HarvestAPI Git Repository"
date:   2014-11-24 11:31:00
categories: jekyll update
---

On November 24, 2014 I worked on transferring HarvestAPI demo to the main HarvestAPI git repository. The first task I did was to 
change the CSS features utilizing the bootstrap css that controls the class tag `form-control` and layouts which were replicatable 
to the ones I did for HarvestAPI demo (<a> http://badbruce07.github.io/harvest-demo2/ </a>).
<br/><br/>
Looking at the `views.py` file, there are various functions consisting of:
<ul>
	<li> FarmerViewSet </li>
	<li> UserViewSet </li>
	<li> ReceiptFilter </li>
	<li> ReceiptViewSet </li>
	<li> FarmFilter </li>
	<li> FarmViewSet </li>
	<li> CropFilter </li>
	<li> CropViewSet </li>
	<li> LivestockFilter </li>
	<li> PriceFilter </li>
	<li> PriceViewSet </li>
	<li> register (which is restricted to `@api_view(['POST'])`) </li>
</ul>
<br/><br/>
After several researching in modifying the fields in the `registration_form.html` file in the `templates` folder, I was required to 
write a `forms.py` file which control each of the fields in the signup tab, made another register function 
in views.py which is grabbing information from the forms.py file and add the register function to the `urls.py` file.