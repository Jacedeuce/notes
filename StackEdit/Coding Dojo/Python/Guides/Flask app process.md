## Steps to create new Flask App

### Project Initialization

1. Make new folder for project
2. Open VSCode and ensure terminal is in the project folder
3. ~`conda activate CD`~ (Only if you're using conda environments)
4. `python -m venv {project_name+Env}`
5. `{project_name+Env}\Scripts\activate`
6. `pip install flask`
7. ___create___ _`app.py`_
	```python
	from flask import Flask, render_template
	app = Flask(__name__)
	
	@app.route("/")
	def index():
		return render_template("index.html")

	if __name__=="__main__":
		app.run(debug=True)
	```
8. ___create___ `templates\index.html`
9. ___create___ `static\css\styles.css`
	add:
	* `<link rel="stylesheet" type="text/css" href="{{ url_for('static', filename='css/styles.css') }}">` 
	* `<link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.3.1/css/bootstrap.min.css" integrity="sha384-ggOyR0iXCbMQv3Xipma34MD+dH/1fQ784/j6cY/iJTQUOhcWr7x9JvoRxT2MZw1T" crossorigin="anonymous">`
10. ___create___ initial packages list `pip freeze > requirements.txt`
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTIyODA2OTU0NF19
-->