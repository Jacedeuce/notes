## Steps to create new Flask App

### Project Initialization

1. Make new folder for project
2. Open VSCode and ensure terminal is in the project folder
3. `conda activate CD`
4. `python -m venv {project_name+Env}`
5. `{project_name+Env}\Scripts\activate`
6. `pip install flask`
7. create _`app.py`_
	```python
	from flask import Flask, render_template
	app = Flask(__name__)
	
	@app.route("/")
	def index():
		return render_template("index.html")

	if __name__=="__main__":
		app.run(debug=True)
	```
8. create `templates\index.html`
9. create `static\css\styles.css`
	add
	`<link rel="stylesheet" type="text/css" href="{{ url_for('static', filename='css/styles.css') }}"` 
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE4ODUzNDM1MjUsMTA4OTEzMDYxLDI0Mj
I4MzYyNF19
-->