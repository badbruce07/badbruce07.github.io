---
layout: post
title:  "HarvestAPI for Mobile and Tablet"
date:   2014-11-06 11:31:00
categories: jekyll update
---

On November 6, 2014, I worked on the media min-width size for each device. One example of this is shown below:
<br/><br/>

{% highlight css %}

@media(min-width:768px) {
	
	#top_panel{
		margin-left: auto;
		margin-right: auto;
	}
   
   header {
   	text-align: center;
    	color: #000;
    	background-attachment: scroll;
    	background-image: url(../img/vector_bg.png);
    	background-position: center center;
    	background-repeat: none;
		width: 768px;
    	-webkit-background-size: cover;
    	-moz-background-size: cover;
    	background-size: cover;
    	-o-background-size: cover;
    	margin-left: auto;
    	margin-right: auto;
	}
	
	header .intro-text .intro-heading {
        margin-bottom: 50px;
        margin-left: auto;
        margin-right: auto;
        text-transform: uppercase;
        font-family: Montserrat,"Helvetica Neue",Helvetica,Arial,sans-serif;
        font-size: 25px;
        font-weight: 700;
        line-height: 50px;
        color: #fff;
        background-color: rgba(0, 0, 0, 0.1); 
	}
   
    
   #header_col{
		color: #006400;
	}
	
	.navbar-default {
        padding: 25px 0;
        border: 0;
        background-color: transparent;
        -webkit-transition: padding .3s;
        -moz-transition: padding .3s;
        transition: padding .3s;
	}
    
	.navbar-default .navbar-nav>.active>a {
		border-radius: 3px;
 	}

	.navbar-default.navbar-shrink {
   	padding: 10px 0;
      background-color: #FFD700;	
      height: 10px;
      margin-left: auto;
      margin-right: auto;
	}
	
	.harvest_icon{
		width:100px;
		height: 60px;
		margin-left: -15px;
		margin-bottom: 15px;
		margin-top: -50px;	
	}
	
	.navbar-default.navbar-shrink .navbar-brand img.harvest_icon{
		width:100px;
		height: 60px;
		margin-left: -15px;
		margin-top: -33px;
	}
    
	.navbar-shrink .nav ul a {
   	text-transform: uppercase;
   	font-family: Montserrat,"Helvetica Neue",Helvetica,Arial,sans-serif;
   	font-weight: 400;
   	letter-spacing: 1px;
   	color: #fff;
   	margin-top: -20px;
   	height: 50px;
   	margin-left: -50px;
	}
    
	#github_link{
		position: relative;
		height: 100px;
		width: 100px;
		margin-left:640px;
		margin-top: -10px;
	} 
	
	img.spons{
		width: 768px;
		margin-left: auto;
    	margin-right: auto;	
	}

}

{% endhighlight%}

Its view looks a lot like this:
![My helpful screenshot]({{ site.url }}/assets/harvest768-view.png)