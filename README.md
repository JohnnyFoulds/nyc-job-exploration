# New York City Current Job Postings Exploration
This project uses Apache Spark to explore the popular New York City Current Job Postings [Kaggle dataset](https://www.kaggle.com/new-york-city/new-york-city-current-job-postings).

[Apache Zeppelin](https://zeppelin.apache.org/) notebooks are used to work interactively with the data, please refer to the [Wiki](https://github.com/JohnnyFoulds/nyc-job-exploration/wiki) for details of how a development environment was configured for use in this project.

## Notebooks
- [Hello World](https://www.zepl.com/viewer/github/JohnnyFoulds/nyc-job-exploration/blob/master/zeppelin/notebook/hello-world/note.json) - This is a basic notebook to make sure Apache Spark is working and include a simple word count example.
- [Word Cloud](https://www.zepl.com/viewer/github/JohnnyFoulds/nyc-job-exploration/blob/master/zeppelin/notebook/word-cloud/note.json) - This notebook demonstrates how do do a simple word cloud with the D3.js library.
- [Spark Core](https://www.zepl.com/viewer/github/JohnnyFoulds/nyc-job-exploration/blob/master/zeppelin/notebook/spark-core/note.json) - Simple reference snippets for Apche Spark Core.

## Zeppelin Word Cloud
It is quite useful to draw a word cloud of text data such as of the job descriptions. The [word-cloud](https://github.com/JohnnyFoulds/nyc-job-exploration/tree/master/zeppelin/notebook/word-cloud) notebook illustrated how this can be done with a limited amount of code with D3.js and two additional external JavaScipt files.

```js
println("%html")
println("<script>")
println("    var wordCollection = [")

textRdd.collect.foreach(t=>
    println("{text: \"" + t._1 + "\", size: " + t._2 * 5 + "},")
)

println("    ]")
println("</script>")
```

```html
print(s"""%html
	<script src="http://d3js.org/d3.v3.min.js"></script>
	<script src="https://cdn.statically.io/gh/JohnnyFoulds/nyc-job-exploration/b9cd4af7/zeppelin/notebook/word-cloud/js/d3.layout.cloud.js"></script>
	<script src="https://cdn.statically.io/gh/JohnnyFoulds/nyc-job-exploration/b9cd4af7/zeppelin/notebook/word-cloud/js/word.cloud.js"></script>
		
	<div id="wordCloud"></div>
	<script>
		//Create a new instance of the word cloud visualisation.
		var myWordCloud = wordCloud('#wordCloud');
		myWordCloud.update(wordCollection);
	</script>
""")
```

The `d3.layout.cloud.js` library is taken from https://github.com/jasondavies/d3-cloud.
