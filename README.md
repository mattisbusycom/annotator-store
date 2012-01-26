# Annotator Store

This is a backend store for the [Annotator][ann].

## Getting going

You'll need a recent version of [Python][1] (>=2.6) and [CouchDB][2] (>=1.0)
installed.

[ann]: http://okfnlabs.org/annotator/
[1]: http://python.org
[2]: http://couchdb.apache.org

The quickest way to get going assumes you have the `pip` and `virtualenv` tools
installed (protip: `easy_install virtualenv` will get them both). Run the
following in the repository root:

    pip -E pyenv install -e .
    source pyenv/bin/activate
    cp annotator.cfg.example annotator.cfg
    python run.py

You should see something like:

    * Running on http://127.0.0.1:5000/
    * Restarting with reloader...

## Store API

The Store API is designed to be compatable with the [Annotator][ann].

### REST API

The annotation store, a JSON-speaking REST API, will be mounted at
`http://localhost:5000/annotations`. You can test this by running:

    $ curl -i http://localhost:5000/annotations
    HTTP/1.0 200 OK
    Content-Type: application/json
    Access-Control-Allow-Origin: *
    Access-Control-Expose-Headers: Location
    Access-Control-Allow-Methods: GET, POST, PUT, DELETE
    Access-Control-Max-Age: 86400
    Content-Length: 2
    Server: Werkzeug/0.6.2 Python/2.6.1
    Date: Fri, 10 Dec 2010 11:44:33 GMT

    []

The "[]" at the end indicates the empty list for your annotations. There are no
annotations currently in the store. See the [Annotator repository][ann] for
details on getting an annotator talking to this backend.

Here's an example of putting an annotation in the store::

    $ curl -X POST http://localhost:5000/annotations -H "Content-Type: application/json" -d '{"text": "abc"}'
    {
      ...
      "text": "abc", 
      "id": 42
      ...
    }

And then we could retrieve this with the command:

    $ curl http://localhost:5000/annotations/42

### Search

You can search annotations in the store via the search api mounted at
`http://localhost:5000/search`. You can test this by running:

    $ curl -i http://localhost:5000/search

The search supports search and offset parameters:

    $ curl -i http://localhost:5000/search?limit=5&offset=2

You can filter on any attribute of an annotation:

    $ curl -i http://localhost:5000/search?uri=myuri

And you can combine filters:

    $ curl -i http://localhost:5000/search?uri=myuri&user=myuser

## Running tests

Running `pip -E pyenv install -e .` or similar, as described above,
should have installed `nosetests` for you. In the virtualenv, you should
be able to run the tests as follows:

    $ nosetests
    .....................
    ----------------------------------------------------------------------
    Ran 21 tests in 0.502s

    OK

Please [open an issue](annotator-store/issues) if you find that the tests
don't all pass on your machine, making sure to include the output of `pip
freeze`.
