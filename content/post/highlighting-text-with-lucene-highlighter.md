---
title: "Highlighting Text With Lucene Highlighter"
date: 2012-04-21T22:15:50+11:00
draft: false
tags: ["highlight", "java", "lucene"]
---

I have a chance to use Lucene (3.6.0) to implement a full-text search in one of my recent projects. One of the requirements is to highlight the matched text in the result. The highlighted text should be displayed in the whole paragraph (not just a small text fragment). Here is my snippet to achieve this:

```java
private String getHighlightedField(Query query, Analyzer analyzer, String fieldName, String fieldValue) throws IOException, InvalidTokenOffsetsException {
    Formatter formatter = new SimpleHTMLFormatter("<span class=\"MatchedText\">", "</span>");
    QueryScorer queryScorer = new QueryScorer(query);
    Highlighter highlighter = new Highlighter(formatter, queryScorer);
    highlighter.setTextFragmenter(new SimpleSpanFragmenter(queryScorer, Integer.MAX_VALUE));
    highlighter.setMaxDocCharsToAnalyze(Integer.MAX_VALUE);
    return highlighter.getBestFragment(this.analyzer, fieldName, fieldValue);
}
```
 

* By creating a `SimpleSpanFragmenter` with a very big fragment size, we can display the highlighted text in the whole paragraph or document. Lucene also does a nice thing here for free, by merging all the highlighted text fragments into one big chunk (or our original paragraph/document).
* `query`: is the Lucene query you constructed to do the search.
* `analyzer`: is the Lucene analyzer are used to analyzed the field when you create the index for that field.

Happy highlighting!

