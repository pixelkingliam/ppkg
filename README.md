# ppkg File Format Specification

## Version: 1.0.0

The ppkg (Portable Package) file format is a container format for storing compressed data along with metadata. This specification defines the structure and usage of ppkg files without reference to any specific implementation.

### File Format Overview

A ppkg file consists of the following components:

1. **Magic Bytes**: A 4-byte sequence that serves as a signature to identify the file format. It is always set to `"ppkg"` in UTF-8-encoded bytes.

2. **Metadata Length**: A 4-byte integer indicating the length of the metadata section in bytes. This length is encoded in little-endian format.

3. **Metadata**: A JSON-formatted metadata section containing information about the package.

4. **Compressed Data**: The compressed data payload of the package.

### Metadata Format

The metadata section is a JSON object with the following structure:

```json
{
  "PackageName": "Pixel.Pkg",
  "PackageVersion": "2.0.0",
  "PackageLicense": "MIT",
  "PackageDescription": "C# Implementation of the ppkg file format",
  "AuthorName": "Pixel",
  "AuthorContacts": null,
  "FormatVersion": "1.0.0",
  "Type": null,
  "MetaMeta": null
}
```

- `PackageName` (string): The name of what's packaged.
- `PackageVersion` (string): The version of what's packaged.
- `PackageLicense` (string): The license of what's packaged.
- `PackageDescription` (string): What's packaged, in more details.
- `AuthorName` (string): The author of the package.
- `AuthorContacts` (string[]): The contact(s) of the author (can also be used for multiple authors.
- `FormatVersion` (string): A version string specifying the format version of the ppkg file.
- `Type` (string): What kind of additional metadata this package contains.
- `MetaMeta` (object): Additional metadata fields included as needed for specific applications or use cases.

### Creating a ppkg File

To create a ppkg file, follow these steps:

1. Create the metadata object as a JSON-formatted string.

2. Encode the metadata object in UTF-8 to obtain the metadata bytes.

3. Compress the data that you want to package using the Deflate compression algorithm.

4. Concatenate the magic bytes, metadata length (encoded in little-endian), metadata bytes, and compressed data.

### Reading a ppkg File

To read a ppkg file, follow these steps:

1. Read the first 4 bytes to verify that they match the magic bytes `"ppkg"` in UTF-8-encoded bytes.

2. Read the next 4 bytes as an integer to determine the length of the metadata section.

3. Read the next `metadata_length` bytes as the metadata section in UTF-8 format.

4. Deserialize the metadata JSON to obtain package metadata.

5. Read the remaining bytes as the compressed data payload.


---
This specification defines the ppkg file format, allowing interoperability across different programming languages and platforms. Implementations in various languages can use this specification as a reference to create and read ppkg files.
