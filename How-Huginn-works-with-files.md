**Note**: This is not available yet: https://github.com/cantino/huginn/pull/1301

### FileHandling

Huginn stores the event payload in a database, to avoid serializing binary data and writing megabytes of data into the database Huginn uses the concept of "file pointers". The pointer is a small JSON structure including the source Agent and the path to the file. Source Agents emit events which only the file pointer, not the actual contents of the file, consuming agents use the pointer to read the file contents and process the data.

### Source Agents

Currently Huginn has three source agents: `LocalFileAgent`, `FtpsiteAgent` and `S3Agent`.

### Consuming Agents

The `ReadFileAgent` reads the file pointer it receives and emits the contents of the file as a new event. The `CsvAgent` can parse large files efficiently by reading the contents per line.