---
layout: post
title:  "Merging HarvestAPI demo To The HarvestAPI Git Repository (Cont'd)"
date:   2014-11-25 11:31:00
categories: jekyll update
---

On November 25, 2014 I began creating the `forms.py` file that controls the field of the registration form in the 
`registration_form.html` file. I had to be sure to use the bootstrap css class tag called `form-class` which makes
the appearance of the input box shown in the <a href="http://badbruce07.github.io/harvest-demo2/"> HarvestAPI Demo Page </a>. 
The fields appear like this in the snippet below:

{% highlight python %}

import re
from django import forms
from django.contrib.auth.models import User
from django.core import validators
from django.utils.translation import ugettext_lazy as _

class RegistrationForm(forms.Form):
    username = forms.CharField(
                widget = forms.TextInput
                        (attrs = {'class': "form-control",
                                  'placeholder': 'Username *'}))

    email= forms.EmailField(
            widget = forms.TextInput
                    (attrs = {'class': "form-control",
                              'placeholder': 'Email *'}))

    password1 = forms.CharField(
                widget = forms.PasswordInput
                        (attrs = {'class': "form-control",
                                  'placeholder': 'Password *'}))

    password2 = forms.CharField(
                widget = forms.PasswordInput
                        (attrs = {'class': "form-control",
                                  'placeholder': 'Repeat Password *'}))
    class Meta:
        model = User
        fields = ["username", "email", "password1", "password2"]

{% endhighlight %}