---
layout: post
title: 总结整理：Apache IOUtils
categories:
    - java
tags:
    - java
    - FileUtils
excerpt: Apache IOUtils方法整理
---

## 转成缓冲流

* static BufferedInputStream	 `buffer(InputStream inputStream) `：Returns the given InputStream if it is already a BufferedInputStream, otherwise creates a BufferedInputStream from the given InputStream.

* static BufferedInputStream	 `buffer(InputStream inputStream, int size)`：Returns the given InputStream if it is already a BufferedInputStream, otherwise creates a BufferedInputStream from the given InputStream.

* static BufferedOutputStream	 `buffer(OutputStream outputStream) `：Returns the given OutputStream if it is already a BufferedOutputStream, otherwise creates a BufferedOutputStream from the given OutputStream.

* static BufferedOutputStream	 `buffer(OutputStream outputStream, int size)`：Returns the given InputStream if it is already a BufferedInputStream, otherwise creates a BufferedInputStream from the given InputStream.

* static BufferedReader	 `buffer(Reader reader) `：Returns the given reader if it is already a BufferedReader, otherwise creates a BufferedReader from the given reader.

* static BufferedReader	 `buffer(Reader reader, int size)`：Returns the given reader if it is already a BufferedReader, otherwise creates a BufferedReader from the given reader.

* static BufferedWriter	 `buffer(Writer writer) `：Returns the given Writer if it is already a BufferedWriter, otherwise creates a BufferedWriter from the given Writer.

* static BufferedWriter	 `buffer(Writer writer, int size)`：Returns the given Writer if it is already a BufferedWriter, otherwise creates a BufferedWriter from the given Writer.

## 关闭文件

* static void	 `close(URLConnection conn)`：Closes a URLConnection.

* static void	 `closeQuietly(Closeable... closeables)`：Closes a Closeable unconditionally.

* static void	 `closeQuietly(Closeable closeable)`：Closes a Closeable unconditionally.

* static void	 `closeQuietly(InputStream input)`：Closes a Closeable unconditionally.

* static void	 `closeQuietly(OutputStream output)`：Closes an OutputStream unconditionally.

* static void	 `closeQuietly(Reader input)`：Closes an Reader unconditionally.

* static void	 `closeQuietly(Selector selector)`：Closes a Selector unconditionally.

* static void	 `closeQuietly(ServerSocket sock)`：Closes a ServerSocket unconditionally.

* static void	 `closeQuietly(Socket sock)`：Closes a Socket unconditionally.

* static void	 `closeQuietly(Writer output)`：Closes an Writer unconditionally.

## 判断文件内容是否相等

* static void	 `contentEquals(InputStream input1, InputStream input2)`：Compares the contents of two Streams to determine if they are equal or not.

* static void	 `contentEquals(Reader input1, Reader input2)`：Compares the contents of two Readers to determine if they are equal or not.

* static void	 `contentEqualsIgnoreEOL(Reader input1, Reader input2)`：Compares the contents of two Readers to determine if they are equal or not, ignoring EOL characters.

## 文件拷贝

* static void	 `copy(InputStream input, OutputStream output)`：Copies bytes from an InputStream to an OutputStream.

* static void	 `copy(InputStream input, OutputStream output, int bufferSize)`：Copies bytes from an InputStream to an OutputStream using an internal buffer of the given size.

* static void	 `copy(InputStream input, Writer output, String inputEncoding)`：Copies bytes from an InputStream to chars on a Writer using the specified character encoding.

* static void	 `copy(Reader input, OutputStream output, Charset outputEncoding)`：Copies chars from a Reader to bytes on an OutputStream using the specified character encoding, and calling flush.

* static void	 `copy(Reader input, OutputStream output, String outputEncoding)`：Copies chars from a Reader to bytes on an OutputStream using the specified character encoding, and calling flush.

* static int	 `copy(Reader input, Writer output)`：Copies chars from a Reader to a Writer.

* static long	 `copyLarge(InputStream input, OutputStream output)`：Copies bytes from a large (over 2GB) InputStream to an OutputStream.

* static long	 `copyLarge(InputStream input, OutputStream output, byte[] buffer)`：Copies bytes from a large (over 2GB) InputStream to an OutputStream.

* static long	 `copyLarge(InputStream input, OutputStream output, long inputOffset, long length)`：Copies some or all bytes from a large (over 2GB) InputStream to an OutputStream, optionally skipping input bytes.

* static long	 `copyLarge(InputStream input, OutputStream output, long inputOffset, long length, byte[] buffer)`：Copies some or all bytes from a large (over 2GB) InputStream to an OutputStream, optionally skipping input bytes.

* static long	 `copyLarge(Reader input, Writer output)`：Copies chars from a large (over 2GB) Reader to a Writer.

* static long	 `copyLarge(Reader input, Writer output, char[] buffer)`：Copies chars from a large (over 2GB) Reader to a Writer.

* static long	 `copyLarge(Reader input, Writer output, long inputOffset, long length)`：Copies some or all chars from a large (over 2GB) InputStream to an OutputStream, optionally skipping input chars.

* static long	 `copyLarge(Reader input, Writer output, long inputOffset, long length, char[] buffer)`：Copies some or all chars from a large (over 2GB) InputStream to an OutputStream, optionally skipping input chars.

## 文件读取

* static LineIterator	 `lineIterator(InputStream input, Charset encoding)`：Returns an Iterator for the lines in an InputStream, using the character encoding specified (or default encoding if null).

* static LineIterator	 `lineIterator(InputStream input, String encoding)`：Returns an Iterator for the lines in an InputStream, using the character encoding specified (or default encoding if null).

* static LineIterator	 `lineIterator(Reader reader)`：Returns an Iterator for the lines in a Reader.

* static int	 `read(InputStream input, byte[] buffer)`：Reads bytes from an input stream.

* static int	 `read(InputStream input, byte[] buffer, int offset, int length)`：Reads bytes from an input stream.

* static int	 `read(Reader input, char[] buffer)`：Reads characters from an input character stream.

* static int	 `read(Reader input, char[] buffer, int offset, int length)`：Reads characters from an input character stream.

* static List<String>	 `readLines(InputStream input, Charset encoding)`：Gets the contents of an InputStream as a list of Strings, one entry per line, using the specified character encoding.

* static List<String>	 `readLines(InputStream input, String encoding)`：Gets the contents of an InputStream as a list of Strings, one entry per line, using the specified character encoding.

* static List<String>	 `readLines(Reader input)`：Gets the contents of a Reader as a list of Strings, one entry per line.

## 类型转换

* static InputStream	 `toBufferedInputStream(InputStream input)`：Fetches entire contents of an InputStream and represent same data as result InputStream.

* static InputStream	 `toBufferedInputStream(InputStream input, int size)`：Fetches entire contents of an InputStream and represent same data as result InputStream.

* static BufferedReader	 `toBufferedReader(Reader reader)`：Returns the given reader if it is a BufferedReader, otherwise creates a BufferedReader from the given reader.

* static BufferedReader	 `toBufferedReader(Reader reader, int size)`：Returns the given reader if it is a BufferedReader, otherwise creates a BufferedReader from the given reader.

* static byte[]	 `toByteArray(InputStream input)`：Gets the contents of an InputStream as a byte[].

* static byte[]	 `toByteArray(InputStream input, int size)`：Gets the contents of an InputStream as a byte[].

* static byte[]	 `toByteArray(InputStream input, long size)`：Gets contents of an InputStream as a byte[].

* static byte[]	 `toByteArray(Reader input, Charset encoding)`：Gets the contents of a Reader as a byte[] using the specified character encoding.

* static byte[]	 `toByteArray(Reader input, String encoding)`：Gets the contents of a Reader as a byte[] using the specified character encoding.

* static byte[]	 `toByteArray(URI uri)`：Gets the contents of a URI as a byte[].

* static byte[]	 `toByteArray(URL url)`：Gets the contents of a URI as a byte[].

* static byte[]	 `toByteArray(URLConnection urlConn)`：Gets the contents of a URLConnection as a byte[].

* static char[]	 `toCharArray(InputStream is, Charset encoding)`：Gets the contents of an InputStream as a character array using the specified character encoding.

* static char[]	 `toCharArray(InputStream is, String encoding)`：Gets the contents of an InputStream as a character array using the specified character encoding.

* static char[]	 `toCharArray(Reader input)`：Gets the contents of a Reader as a character array.

* static InputStream	 `toInputStream(String input, Charset encoding)`：Converts the specified string to an input stream, encoded as bytes using the specified character encoding.

* static InputStream	 `toInputStream(String input, String encoding)`：Converts the specified string to an input stream, encoded as bytes using the specified character encoding.

* static String	 `toString(byte[] input, String encoding)`：Gets the contents of a byte[] as a String using the specified character encoding.

* static String	 `toString(InputStream input, Charset encoding)`：Gets the contents of an InputStream as a String using the specified character encoding.

* static String	 `toString(InputStream input, String encoding)`：Gets the contents of an InputStream as a String using the specified character encoding.

* static String	 `toString(Reader input)`：Gets the contents of a Reader as a String.

* static String	 `toString(URI uri, Charset encoding)`：Gets the contents at the given URI.

* static String	 `toString(URI uri, String encoding)`：Gets the contents at the given URI.

* static String	 `toString(URL url, Charset encoding)`：Gets the contents at the given URI.

* static String	 `toString(URL url, String encoding)`：Gets the contents at the given URL.

## 写文件

* static void	 `write(byte[] data, OutputStream output)`：Writes bytes from a byte[] to an OutputStream.

* static void	 `write(byte[] data, Writer output, Charset encoding)`：Writes bytes from a byte[] to chars on a Writer using the specified character encoding.

* static void	 `write(byte[] data, Writer output, String encoding)`：Writes bytes from a byte[] to chars on a Writer using the specified character encoding.

* static void	 `write(char[] data, OutputStream output, Charset encoding)`：Writes chars from a char[] to bytes on an OutputStream using the specified character encoding.

* static void	 `write(char[] data, OutputStream output, String encoding)`：Writes chars from a char[] to bytes on an OutputStream using the specified character encoding.

* static void	 `write(char[] data, Writer output)`：Writes chars from a char[] to a Writer

* static void	 `write(String data, OutputStream output, Charset encoding)`：Writes chars from a String to bytes on an OutputStream using the specified character encoding.

* static void	 `write(String data, OutputStream output, String encoding)`：Writes chars from a String to bytes on an OutputStream using the specified character encoding.

* static void	 `write(String data, Writer output)`：Writes chars from a String to a Writer.

* static void	 `writeLines(Collection<?> lines, String lineEnding, OutputStream output, Charset encoding)`：Writes the toString() value of each item in a collection to an OutputStream line by line, using the specified character encoding and the specified line ending.

* static void	 `writeLines(Collection<?> lines, String lineEnding, OutputStream output, String encoding)`：Writes the toString() value of each item in a collection to an OutputStream line by line, using the specified character encoding and the specified line ending.

* static void	 `writeLines(Collection<?> lines, String lineEnding, Writer writer)`：Writes the toString() value of each item in a collection to a Writer line by line, using the specified line ending.
