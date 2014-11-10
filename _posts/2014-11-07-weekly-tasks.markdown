---
layout: post
title:  "HarvestAPI for Mobile and Tablet Cont'd"
date:   2014-11-07 11:31:00
categories: jekyll update
---

On November 7, 2014 I continued working on the CSS media width size for each device. There are some that I created as shown below.
Yesterday I had created CSS for `media min-width size 768px`. Now there are a few more others:

{% highlight css %}

@media(min-width:655px){
	
	.harvest_icon{
		height: 60px;
		width: 120px;
		margin-top: -20px;	
	}
	
	.navbar-shrink .navbar-brand img.harvest_icon{
		height: 60px;
		width: 120px;
		margin-top: -20px;
		margin-left: 0;
	}
	
	#move-button{
		margin-top: 100px;	
	
	}
	#info_farm{
		margin-top: 200px;
	}

	.btn-xl {
    padding: 10px 10px;
    border-color: #{{ site.color.primary }};
    border-radius: 3px;
    text-transform: uppercase;
    font-family: Montserrat,"Helvetica Neue",Helvetica,Arial,sans-serif;
    font-size: 12px;
    font-weight: 700;
    color: #fff;
    background-color: #{{ site.color.primary }};
	}
	
	header {
   	text-align: center;
    	color: #000;
    	background-attachment: scroll;
    	background-image: url(../img/vector_bg.png);
    	background-position: center center;
    	background-repeat: none;
    	width: 655px;
    	-webkit-background-size: cover;
    	-moz-background-size: cover;
    	background-size: cover;
    	-o-background-size: cover;
    	margin-left: auto;
    	margin-right: auto;
	}
	
	#header_col{
		color: white;
	}

	.bg-blue{
		background-color: #3FADA4;
		width: 655px;
		margin-left: auto;
   	margin-right: auto;
	}
	
	.bg-light-gray {
    	background-color: #6ACD7C;
    	width: 655px;
   	margin-left: auto;
    	margin-right: auto;
	}
	
	section.bg-white{
		background-color: #FFFFFF;
		width: 655px;
   	margin-left: auto;
    	margin-right: auto;
	}
	
	img.spons{
		width: 655px;
		margin-left: auto;
    	margin-right: auto;	
	}
	
	header .intro-text .intro-heading {
        margin-bottom: 0;
        margin-top: 400px;
        text-transform: uppercase;
        font-family: Montserrat,"Helvetica Neue",Helvetica,Arial,sans-serif;
        font-size: 20px;
        font-weight: 700;
        line-height: 50px;
        color: #fff;
        background-color: rgba(0, 0, 0, 0.1); 
    }	
	
}
{% endhighlight %}