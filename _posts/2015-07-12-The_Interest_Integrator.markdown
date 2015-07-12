---
layout: post
title:  "The Interest Integrator"
date:   2015-07-12 14:48:00
categories: code
---
A while ago I read the book [Mindhacker](http://www.wiley.com/WileyCDA/WileyTitle/productCd-1118007522.html) by Ron Hale-Evans and Mary Hale-Evans.

There was a cool script listed called the *interest integrator*: A simple perl script that runs google searches for two search terms located in an 'interests file' with the intent of yielding new and interesting combinations of topics you might be interested in. An example search generated might be:

```
http://www.google.com/search?num=100&q=jekyll+blogging
```

Anyway, recently I was thinking about the book and decided to try the script. I had to mess with it a bit to get it to run on the Mac, but here is the modified version of the original.

{% highlight perl %}
#!/usr/bin/perl
# ii, Interest Integrator
# Ron Hale-Evans, rwhe@ludism.org
# 2010-05-20

$nargs = $#ARGV + 1;
srand;

# You may need to adjust the following values,
# depending on your environment
$home = $ENV{HOME};
$obsessions = "obsessions.txt";
#$browser = "firefox";
#$browser = "google-chrome";
$browser = "open";

# Usage information
if ($nargs > 2)
{
    $two = "\"ii chimp hilarious-consequences\" googles both terms.";
    $one = "\"ii chimp\" googles \"chimp\" plus a random obsession.";
    $zero = "\"ii\" by itself googles two random obsessions.";
    die "usage:\n$two\n$one\n$zero\n";
}
elsif ($nargs == 2)
{
    $arg1 = $ARGV[0];
    $arg2 = $ARGV[1];
}
elsif ($nargs == 1)
{
    $arg1 = $ARGV[0];
    $arg2 = random_obsession();
}
else
{
    $arg1 = random_obsession();
    $arg2 = random_obsession();
}

$arg1 = munge($arg1);
$arg2 = munge($arg2);

$url = "http://www.google.com/search?num=100&q=$arg1+$arg2";
print "$url\n";
`$browser '$url'`;

sub random_obsession()
{
    open FILE, "<$obsessions" or die "Could not open obsessions.txt: $!\n";
    rand($.) <1 and ($line=$_) while <FILE>;
    close FILE;
    return($line);
}

# Tweak the search terms so they can form part of a valid URL
sub munge($)
{
    my ($a) = @_;

    chomp($a);
    $a =~ s/\"/\%22/sgi;
    $a =~ s/\+/\%2B/sgi;
    $a =~ s/ /\+/sgi;

    return($a);
}
{% endhighlight %}
