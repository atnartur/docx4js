#docx4js
a javascript docx parser

#install
	$ npm install docx4js
	
#license
GPL

#API
```html
	<head>
		<script src="../dist/docx4js.js"></script>
		<script>
			var DOCX=require('docx4js')
			var converter=[]
			converter.visit=function(){
				if(this.model.type=='paragraph')
					return this.push("\n\r")
				if(this.model.type=='text')
					return this.push(this.model.getText())
			}

			function test(input){
				converter.splice(0,converter.length)
				DOCX.load(input.files[0])
					.then(function(doc){
						input.value=""
						document.$1('body>pre').innerHTML=""
						doc.parse(DOCX.createVisitorFactory(), DOCX.createVisitorFactory(function(srcModel){
							converter.model=srcModel
							return converter;
						}))
						document.$1('body>pre').innerHTML=converter.join('')
					})
			}
		</script>
	</head>
	<body>
		<input type="file" style="position:absolute;top:0" onchange="test(this)">
		<pre></pre>
	</body>
```

