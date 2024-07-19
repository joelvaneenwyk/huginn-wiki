### File Handling

Huginn stores Event payloads in a database. To avoid serializing binary data and writing megabytes of data into the database, Huginn uses the concept of "file pointers". A file pointer is a small JSON structure that is added to an Event, including the source Agent and a "path" to the file data. Source Agents emit Events with only the file pointer, not the actual contents of the file, consuming Agents use the pointer to read the file contents and process the data.

### Source Agents

Currently Huginn has three file pointer source agents: `LocalFileAgent`, `FtpsiteAgent` and `S3Agent`.

### Consuming Agents

The `ReadFileAgent` can read a file pointer it receives and emit the contents of the file as a new event. The `CsvAgent` can parse large files efficiently by reading the contents per line.
