---
layout: post
title:  "Th Grails matches Constraint"
date:   2015-06-05 22:00:00
categories: grails
---
I recently worked on a Grails 2.5.0 application and I was making the wrong assumption that the [matches constraint](https://grails.github.io/grails-doc/2.5.x/ref/Constraints/matches.html) is checked against the domain property all the times so even when its value is blank or null.
 
The field constraint was defined similar to this:  
{% highlight groovy %}
username matches: '[.\\-\\w]+'
{% endhighlight %}

I was expecting the matches constraint to be verified on the username property value. The reality is that when the target property value is blank the matches constraint is never invoked and there are __no errors registered__. The [AbstractConstraint#skipBlankValues()](http://grepcode.com/file/repo1.maven.org/maven2/org.grails/grails-validation/2.5.0/org/codehaus/groovy/grails/validation/AbstractConstraint.java#AbstractConstraint.skipBlankValues%28%29) method returns true by default and [MatchesConstraint](http://grepcode.com/file/repo1.maven.org/maven2/org.grails/grails-validation/2.5.0/org/codehaus/groovy/grails/validation/MatchesConstraint.java#MatchesConstraint) doesn't override it to return false:  
![Constrained property validation]({{ site.url }}/assets/images/grails-constrained-property-validation.png)

To get an error reported for blank values you need to explicitly add the blank constraint:  
{% highlight groovy %}
username matches: '[.\\-\\w]+', blank: false
{% endhighlight %}

While unit testing the constrained property I got into a different issue. There is still an [open bug](https://jira.grails.org/browse/GRAILS-11136) in Grails related to unit testing. If you rely on _grails.databinding.convertEmptyStringsToNull=false_ and _grails.databinding.trimStrings = false_ you need to be aware they're being ignored when running the unit tests. If you create your test fixture objects by means of the Map constructor Grails will populate your objects with null values for any blank Strings: 
{% highlight groovy %}
def user = new User(username: '   ')
assert user.username == null
{% endhighlight %}

There are several workarounds but the easiest is to avoid the data binding in the first place:  
{% highlight groovy %}
def user = new User()
user.username = '   '
assert user.username == '   '
{% endhighlight %}
