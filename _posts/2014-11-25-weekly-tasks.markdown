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
<br/>

I then added a new function in the `views.py` file called `register_here() which has an request parameter which would allow the 
registration_form.html file to redirect to the `registration_complete.htl` page indicating that registration was done successfully.
<br/>
{% highlight python %}

@csrf_protect
def register_here(request):
    """ User sign up form """
    if request.method == 'POST':
        form = RegistrationForm(request.POST)
        if form.is_valid():
            user = User.objects.create_user(
            username = form.cleaned_data['username'],
            email = form.cleaned_data['email'],
            password = form.cleaned_data['password1']
            )
            user = form.save()
            return HttpResponseRedirect( '/registration_complete.html')

    else:
        form = RegistrationForm()

    return render_to_response('../templates/registration/registration_form.html', {'form':form},
                              context_instance=RequestContext(request))
{% endhighlight %}

The HarvestAPI database was made in Postgres-SQL. See <a> http://www.postgresql.org/files/documentation/pdf/9.1/postgresql-9.1-A4.pdf
</a> for the tutorials online. The database name is called `harvest_api`. 

<br/>
When I ran `python manage.py runserver`, I stumbled upon an error called:
{% highlight ruby%}
OperationError: fe_sendauth: no password supplied.
{% endhighlight %}