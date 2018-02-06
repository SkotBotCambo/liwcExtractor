# liwcExtractor
This is a python module that helps conduct analysis based on methods developed by James Pennebaker and the Linguistic Inquiry and Word Count software.  It requires the .dic file that comes with the proprietary LIWC software.

# Using the LIWC extractor
To use this module you need to own a copy of LIWC.  If you do not own a copy, you can purchase one from [LIWC.net](http://www.liwc.net)

Before you begin, you need to locate the LIWC2007_English_plus_txt.dic from the LIWC software.  To do this, you may have to install LIWC after obtaining a license from the LIWC website.

After obtaining a copy of LIWC2007_English_plus_txt.dic you can put it in the directory where the liwcExtractor module exists and use the following code to import liwcExtractor
```
import liwcExtractor as le
liwc = le.liwcExtractor()
```

or you can point to LIWC2007_English_plus_txt.dic in its current directory by using the following code

```
import liwcExtras as le
path_to_liwc = "~/path/to/liwc/LIWC2007_English_plus_txt.dic"
liwc = le.liwcExtractor(liwcPath=path_to_liwc)
```

There are two main methods in liwcExtractor
1. extractFromDoc()
2. extract()

Each of these will return a long array containing liwc features which relate to different categories.  In the interest of being efficient with data structures, you will need to use the getCategoryIndeces() method for a full list of how the indeces in the array relate various liwc categories.

For example, you might have the following corpus...

```
doc1 = "This is the first document that I am going to test with liwcExtractor"
doc2 = "The second one might have some werrrrrrrdddd things in it. ;-)"
doc3 = "The third one.....asdf;lkj;alskjdf;lkjasfd, who even knows. The third makes me want to cry!"
corpus = [doc1, doc2, doc3]
```

you use this code on the third one

```
features = liwc.extractFromDoc(doc3)
```

and get...

```
[0, 1, 1, 3, 1, ...]
```

To understand which categories these are you can do the following

```
categories = liwc.getCategoryIndeces()
```

the <code>categories</code> variable is a list just like <code>features</code> which looks like this...

```
['ingest', 'cause', 'insight', 'cogmech', 'sad', ...]
```

Keep in mind, these are raw counts, unlike what LIWC provides which is a proportion based on the wordcount
To get proportions, you need to divide by the variable in the wordcount index or <code>wc</code> like this...

```
proportions = [x/float(features[66]) for x in features]
```

and you will get...

```
[0.0, 0.041666666666666664, 0.041666666666666664, 0.125, 0.041666666666666664, ...]
```
