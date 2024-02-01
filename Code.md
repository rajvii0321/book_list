from flask import Flask, request, jsonify

app = Flask(__name__)

book_list = [

  {
    "id": 1,
    "author": "Chinua Achebe",
    "language": "English",
    "pages": 209,
    "title": "Things Fall Apart",
  },
  {
    "id": 2,
    "author": "Hans Christian Andersen",
    "language": "Danish",
    "pages": 784,
    "title": "Fairy tales",
  },
  {
    "id": 3,
    "author": "Dante Alighieri",
    "language": "Italian",
    "pages": 928,
    "title": "The Divine Comedy",
  },
  {
    "id": 4,
    "author": "Emily Bront",
    "language": "English",
    "pages": 160,
    "title": "The Epic Of Gilgamesh",
  },
  {
    "id": 5,
    "author": "Jane Austen",
    "language": "English",
    "pages": 226,
    "title": "Pride and Prejudice",
  },
  {
    "id": 6,
    "author": "Paul Celan",
    "language": "German",
    "pages": 320,
    "title": "Poems",
  }

]

@app.route('/books', methods=['GET','POST'])
def books():
    if request.method == 'GET':
        if len(book_list) > 0:
            return jsonify(book_list)
        else:
            'Nothing Found', 404

    if request.method == 'POST':
        new_author = request.form['author']
        new_language = request.form['language']
        new_pages = request.form['pages']
        new_title = request.form['title']
        iD = book_list[-1]['id']+1

        new_obj = {
            'id': iD,
            'author': new_author,
            'language': new_language,
            'pages': new_pages,
            'title': new_title
        }
        book_list.append(new_obj)
        return jsonify(book_list), 201
    
if __name__ == '__main__':
    app.run()
