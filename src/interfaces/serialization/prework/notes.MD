# Serialization

"Serialization of structured data is a key step to transmit information over networks or to store data because is a very cpu-intensive task. Actually, in many communication scenarios the bottleneck is the data serialization and deserialization...Middleware alternatives based on verbose serialization formats such as XML or JSON, used in Web Services and REST, expose very poor performance."
 (src: https://www.eprosima.com/index.php/resources-all/performance/apache-thrift-vs-protocol-buffers-vs-fast-buffers)
 
### Useful terms

IDL - Interface Definition Language

Benefits over JSON/XML:


- forward + backwards compatibility (includes versions, and bc u never directly store field names you're not beholden to them)


## Thrift

"a framework, for implementing RPC in services, with cross-language support."

- DSL: language-agnostic IDL 
- data serialization: binary
- official language support (w varying features): "ActionScript", "C (glib)", "C++", "C#", "Common LISP", "Dlang", "Dart", "Delphi", ".NET Core", ".NET Standard", "Erlang", "Go", "Haskell", "Haxe", "Java (SE)", "Java (ME)", "Javascript", "Lua", "node.js", "node.ts", "OCaml", "Perl", "PHP", "Python", "Ruby", "Rust", "Smalltalk", "Swift" 
- other: cross-language support, compiler generated RPC client code, compiler generated RPC server code: this is a big deal because let's say you are sending the data from a Python app (client) to a Java app (server). If you define all the objects/fns you need with Thrift's IDL, it will compile to the classes/interfaces/etc + the stubbed code you will need to serialize in your Python application and deserialize in your Java application.
- Richer data structures than Protobuf (e.g.: Map and Set)

## Protocol Buffers
method of serializing structured data

- DSL: language-agnostic IDL 
- data serialization: binary wire format or ASCII
- self-describing: yes if ASCII. no if binary -> spec to deserialize does not exist in the file. benefit is space savings bc file only contains the values not the fields
- official language support: Java, Python, C++, Go, Ruby, Objective-C, or C# as of proto3
- other: basis for a custom RPC engine used in nearly all inter-machine communication at Google.

## Avro

- DSL: schemas defined in JSON (don't have to learn a new DSL ala Thrift's IDL, *but* offers experimental Avro IDL if you want that)
- data serialization: compact binary format or JSON (for easier debugging + web-based apps)
- self-describing: file itself contains the schema
- other: can be deserialized without a spec bc it's just JSON
