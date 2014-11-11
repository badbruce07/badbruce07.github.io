---
layout: post
title:  "Tutorials in Using HarvestAPI in PHP (Pt. 1)"
date:   2014-10-07 11:31:00
categories: jekyll update
---

<h2> <b> Getting Connected with HarvestAPI </b> </h2>
<br/>

I started learning PHP with cURL which was very useful to connect PHP with HarvestAPI. I will be using Linux/Ubuntu Operating
System. I had to also install curl in the terminal using the command below:
<br/><br/>
{% highlight ruby %}
sudo apt-get install php5-curl
{% endhighlight %} 

<br/><br/>
and then restart the server using the command: <br/><br/>

{% highlight ruby %}
sudo service apache2 restart
{% endhighlight %} 
<br/><br/>

<h3> <b> How to Create The PHP file to connect to HarvestAPI </b> </h3>  

Now we are at the stage where we need to create a PHP file that will enable connection to HarvestAPI. 
If you are familiar with PHP we can proceed, otherwise check out PHP tutorials at this link: 
<a href="http://www.tutorialspoint.com/php/php_tutorial.pdf" > PHP Tutorials </a>. 
We would also need to get familiar with cURL as well along the way. 
<br/><br/>

<h3> <b> About cURL  </b> </h3>
Now cURL is a command line tool for getting or sending files using URL syntax. <br /><br/>

<h3> <b>About libcURL </b> </h3> 

Libcurl is a free client-side URL transfer library, supporting FTP, FTPS, Gopher, HTTP, 
HTTPS, SCP, SFTP, TFTP, Telnet, DICT, the file URI scheme, LDAP, LDAPS, IMAP, POP3, SMTP and RTSP. 
The library supports HTTPS certificates, HTTP POST, HTTP PUT, FTP uploading, Kerberos, HTTP 
form-based upload, proxies, cookies, user-plus-password authentication, file transfer resume, 
and HTTP proxy tunneling. (from <a>http://en.wikipedia.org/wiki/CURL</a>)
<br /> <br/>

<h3> <b> The relationship between cURL and libcURL </b> </h3> 
				
Since cURL uses libcURL, it supports a range of common Internet protocols, currently including HTTP, 
HTTPS, FTP, FTPS, SCP, SFTP, TFTP, LDAP, LDAPS, DICT, TELNET, FILE, IMAP, POP3, SMTP and RTSP. For HarvestAPI,
it is under HTTP. (from <a>http://en.wikipedia.org/wiki/CURL</a>)
<br /> <br/>

{% highlight PHP%}

<?php

	// Creating a PHP file for calling HarvestAPI
					
	function CallAPI($method, $url, $data = false)
	{
   	$curl = curl_init();

		switch ($method)
		{
   		case "POST":
      		curl_setopt($curl, CURLOPT_POST, 1);

         	if ($data)
         		curl_setopt($curl, CURLOPT_POSTFIELDS, $data);
            	break;
        
    		case "PUT":
      		curl_setopt($curl, CURLOPT_PUT, 1);
      		break;
        
      		default:
      			if ($data)
      				$url = sprintf("%s?%s", $url, http_build_query($data));
		}
	}
	// Optional Authentication:
	curl_setopt($curl, CURLOPT_HTTPAUTH, CURLAUTH_BASIC);
	curl_setopt($curl, CURLOPT_USERPWD, "username:password");

	curl_setopt($curl, CURLOPT_URL, $url);
	curl_setopt($curl, CURLOPT_RETURNTRANSFER, 1);

	$result = curl_exec($curl);

	curl_close($curl);
	return $result;

?>				

{% endhighlight %}

<br/><br/>
Now shown above is a PHP snippet (let's call it CallHarvestAPI.php) containing a function which takes 3 parameters.
<ul>
	<li> $method - This is used to determine whether you are trying to GET, POST, PUT, etc. </li>
	<li> $url - This is referring to the HTTP site that you are using, in this case the HarvestAPI url. </li>
	<li> $data - is set by default as <b>false</b> unless otherwise. </li>					
</ul>				
<br />

In line 7, `curl_init()` is used to initialize a cURL session. <br />
`curl_setopt` is used to set an option for a cURL transfer. It takes 3 parameters, in our case it would be 
`curl_init()` which is defined as the variable $curl, a cURL option which are shown in each case of switch
and a value which can be any variable or number.
<br/>

You have the option to be a user of HarvestAPI simply by going to 
<a href="http://harvestdata.herokuapp.com/user/register"> HarvestAPI</a>	
and click the sign up tab. Once registered, you can use your username and password to replace `username:password` in line 29.
<br/>
In line 34, `curl_exec()` performs the cURL session $curl and stores it in a varible called <b>$result.</b> <br/>
In line 36, `curl_close()` closes the cURL session and in line 37, the <b>$result</b> is returned.	