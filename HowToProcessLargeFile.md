# Introduction #

When reading/writing excel file with POI it consumes a lot of memory for parsing content, making a memory requirement ~3Gb for processing of excel file of size ~20Mb. Provided details below on how to make use of streaming API provided by POI to process large files.

# Details #

There are streaming API which enables streaming for reading and streaming for writing. Streaming allows excel files processing with very low memory footprint.
  * http://poi.apache.org/spreadsheet/how-to.html#event_api
  * http://poi.apache.org/spreadsheet/how-to.html#xssf_sax_api
  * http://poi.apache.org/spreadsheet/how-to.html#sxssf

[sqlsheet](http://code.google.com/p/sqlsheet) starting from [version 6.1](http://sqlsheet.googlecode.com/svn/maven2/com/google/code/sqlsheet/) supports both modes. To enable streaming you need to pass specific preference in JDBC url:

### Read streaming ###
  * Parameter to enable read streaming: **readStreaming**
```
url="jdbc:xls:file:test.xls?readStreaming=true"
```
  * When read streaming enabled - you cannot modify excel file, eow connection is read-only
  * Works for both XLS and XSLX formats

### Write streaming ###
  * Parameter to enable write streaming: **writeStreaming**
```
url="jdbc:xls:file:test.xlsx?writeStreaming=true"
```
  * When write streaming enabled - you cannot query existing excel file, eow connection is write-only
  * You can create tables (sheets) in file using JDBC and write data, each 1k of rows excel file will be flushed to disk and memory cleaned
  * Write streaming works only for XSLX formats
  * You can provide existing file, but only as template which needs to be filled, if you will provide large existing file - you will get memory issue