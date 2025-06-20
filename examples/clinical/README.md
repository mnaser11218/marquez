The files in this directory represent what a multi-job migration from an on-premises file system to Domino by way of an intermediate blob store.

Specifically:
- `tg0014-parent.json` represents the parent job, which is the container for all the child jobs that follow and sets context (study, compound, therapeutic area)
- `legacy-to-blob.json` represents a successful transfer of mixed code and data from an on-premises filesystem to a cloud blob store.
- `blob-to-github.json` represents the successful creation of an as-yet-empty Github repository
- `provision-domino.json` represents the successful creation of a Domino project and datasets linked to the previously-created Git repository
- `populate-code.json` represents the successful population of the `main` branch in the created repository with code from the blob store
- `populate-dataset.json` represents the successful population of the previously-created Domino dataset with clinical data from the blob store

To import these files to a local server running on port 5000, try the following commands in a `bash` shell:
```bash 
curl -X POST -i -H "Content-Type: application/json" -d @./tg0014-parent.json http://localhost:5000/api/v1/lineage

curl -X POST -i -H "Content-Type: application/json" -d @./legacy-to-blob.json http://localhost:5000/api/v1/lineage

curl -X POST -i -H "Content-Type: application/json" -d @./blob-to-github.json http://localhost:5000/api/v1/lineage

curl -X POST -i -H "Content-Type: application/json" -d @./provision-domino.json http://localhost:5000/api/v1/lineage

curl -X POST -i -H "Content-Type: application/json" -d @./populate-code.json http://localhost:5000/api/v1/lineage

curl -X POST -i -H "Content-Type: application/json" -d @./populate-dataset.json http://localhost:5000/api/v1/lineage
```