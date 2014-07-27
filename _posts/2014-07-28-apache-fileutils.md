---
layout: post
title: 总结整理：Apache FileUtils
categories:
    - java
tags:
    - java
    - FileUtils
excerpt: Apache FileUtils方法整理
---

## 设定大小

* static String	 `byteCountToDisplaySize(BigInteger size) `：Returns a human-readable version of the file size, where the input represents a specific number of bytes.

* static String	 `byteCountToDisplaySize(long size)`：Returns a human-readable version of the file size, where the input represents a specific number of bytes.

## 清除目录

* static void	 `cleanDirectory(File directory)`：Cleans a directory without deleting it.

## 判断文件是否相等

* static boolean	 `contentEquals(File file1, File file2)`：Compares the contents of two files to determine if they are equal or not.

* static boolean	 `contentEqualsIgnoreEOL(File file1, File file2, String charsetName)`：Compares the contents of two files to determine if they are equal or not.

## 由集合转成数组

* static File[]	 `convertFileCollectionToFileArray(Collection<File> files)`：Converts a Collection containing java.io.File instanced into array representation.

## 目录拷贝

* static void	 `copyDirectory(File srcDir, File destDir)`：Copies a whole directory to a new location preserving the file dates.

* static void	 `copyDirectory(File srcDir, File destDir, boolean preserveFileDate)`：Copies a whole directory to a new location.

* static void	 `copyDirectory(File srcDir, File destDir, FileFilter filter)`：Copies a filtered directory to a new location preserving the file dates.

* static void	 `copyDirectory(File srcDir, File destDir, FileFilter filter, boolean preserveFileDate)`：Copies a filtered directory to a new location.

* static void	 `copyDirectoryToDirectory(File srcDir, File destDir)`：Copies a directory to within another directory preserving the file dates.

## 文件拷贝

* static void	 `copyFile(File srcFile, File destFile)`：Copies a file to a new location preserving the file date.

* static void	 `copyFile(File srcFile, File destFile, boolean preserveFileDate)`：Copies a file to a new location.

* static long	 `copyFile(File input, OutputStream output)`：Copy bytes from a File to an OutputStream.

* static void	 `copyFileToDirectory(File srcFile, File destDir)`：Copies a file to a directory preserving the file date.

* static void	 `copyFileToDirectory(File srcFile, File destDir, boolean preserveFileDate)`：Copies a file to a directory optionally preserving the file date.

* static void	 `copyInputStreamToFile(InputStream source, File destination)`：Copies bytes from an InputStream source to a file destination.

* static void	 `copyToFile(InputStream source, File destination)`：Copies bytes from an InputStream source to a file destination.

* static void	 `copyURLToFile(URL source, File destination)`：Copies bytes from the URL source to a file destination.

* static void	 `copyURLToFile(URL source, File destination, int connectionTimeout, int readTimeout)`：Copies bytes from the URL source to a file destination.

## 文件删除

* static void	 `deleteDirectory(File directory)`：Copies bytes from the URL source to a file destination`adv. 递归地；递回地`.

* static void	 `deleteQuietly(File file)`：Deletes a file, never throwing an exception.

* static void	 `directoryContains(File directory, File child)`：Determines whether the parent directory contains the child element (a file or directory).

* static void	 `forceDelete(File file)`：Deletes a file.

* static void	 `forceDeleteOnExit(File file)`：Schedules a file to be deleted when JVM exits.

## 目录创建

* static void	 `forceMkdir(File directory)`：Makes a directory, including any necessary but nonexistent parent directories.

* static void	 `forceMkdirParent(File file)`：Makes any necessary but nonexistent parent directories for a given File.

## 文件创建

* static File	 `getFile(File directory, String... names)`：Construct a file from the set of name elements.

* static File	 `getFile(String... names)`：Construct a file from the set of name elements.

## 获取临时文件

* static File	 `getTempDirectory()`：Returns a File representing the system temporary directory.

* static String	 `getTempDirectoryPath()`：Returns the path to the system temporary directory.

* static File	 `getUserDirectory()`：Returns a File representing the user's home directory.

* static String	 `getUserDirectoryPath()`：Returns the path to the user's home directory.

## 比特定时间/文件新(旧)的文件

* static boolean	 `isFileNewer(File file, Date date)`：Tests if the specified File is newer than the specified Date.

* static boolean	 `isFileNewer(File file, File reference)`：Tests if the specified File is newer than the reference File.

* static boolean	 `isFileNewer(File file, long timeMillis)`：Tests if the specified File is newer than the specified time reference.

* static boolean	 `isFileOlder(File file, Date date)`：Tests if the specified File is older than the specified Date.

* static boolean	 `isFileOlder(File file, File reference)`：Tests if the specified File is older than the reference File.

* static boolean	 `isFileOlder(File file, long timeMillis)`：Tests if the specified File is older than the specified time reference.

## 迭代（列出）文件

* static Iterator<File>	 `iterateFiles(File directory, IOFileFilter fileFilter, IOFileFilter dirFilter)`：Allows iteration over the files in given directory (and optionally its subdirectories).

* static Iterator<File>	 `iterateFiles(File directory, String[] extensions, boolean recursive)`：Allows iteration over the files in a given directory (and optionally its subdirectories) which match an array of extensions.

* static Iterator<File>	 `iterateFilesAndDirs(File directory, IOFileFilter fileFilter, IOFileFilter dirFilter)`：Allows iteration over the files in given directory (and optionally its subdirectories).

* static Collection<File>	 `listFiles(File directory, IOFileFilter fileFilter, IOFileFilter dirFilter)`：Finds files within a given directory (and optionally its subdirectories).

* static Collection<File>	 `listFiles(File directory, String[] extensions, boolean recursive)`：Finds files within a given directory (and optionally its subdirectories) which match an array of extensions.

* static Collection<File>	 `listFilesAndDirs(File directory, IOFileFilter fileFilter, IOFileFilter dirFilter)`：Finds files within a given directory (and optionally its subdirectories).

## 移动文件(目录)

* static void	 `moveDirectory(File srcDir, File destDir)`：Moves a directory.

* static void	 `moveDirectoryToDirectory(File src, File destDir, boolean createDestDir)`：Moves a directory to another directory.

* static void	 `moveFile(File srcFile, File destFile)`：Moves a file.

* static void	 `moveFileToDirectory(File srcFile, File destDir, boolean createDestDir)`：Moves a file to a directory.

* static void	 `moveToDirectory(File src, File destDir, boolean createDestDir)`：Moves a file or directory to the destination directory.

## 打开(读取)文件

* static FileInputStream	 `openInputStream(File file)`：Opens a FileInputStream for the specified file, providing better error messages than simply calling new FileInputStream(file).

* static FileOutputStream	 `openOutputStream(File file)`：Opens a FileOutputStream for the specified file, checking and creating the parent directory if it does not exist.

* static FileOutputStream	 `openOutputStream(File file, boolean append)`：Opens a FileOutputStream for the specified file, checking and creating the parent directory if it does not exist.

* static URL[]	 `toURLs(File[] files)`：Converts each of an array of File to a URL.

* static File	 `toFile(URL url)`：Convert from a URL to a File.

* static File[]	 `toFiles(URL[] urls)`：Converts each of an array of URL to a File.

* static byte[]	 `readFileToByteArray(File file)`：Reads the contents of a file into a byte array.

* static String	 `readFileToString(File file, Charset encoding)`：Reads the contents of a file into a String.

* static String	 `readFileToString(File file, String encoding)`：Reads the contents of a file into a String.

* static List<String>	 `readLines(File file, Charset encoding)`：Reads the contents of a file line by line to a List of Strings.

* static List<String>	 `readLines(File file, String encoding)`：Reads the contents of a file line by line to a List of Strings.

## 文件(目录)大小

* static long	 `sizeOf(File file)`：Returns the size of the specified file or directory.

* static BigInteger	 `sizeOfAsBigInteger(File file)`：Returns the size of the specified file or directory.

* static long	 `sizeOfDirectory(File directory)`：Counts the size of a directory recursively (sum of the length of all files).

* static BigInteger	 `sizeOfDirectoryAsBigInteger(File directory)`：Counts the size of a directory recursively (sum of the length of all files).

## 写文件

* static void	 `write(File file, CharSequence data, Charset encoding)`：Writes a CharSequence to a file creating the file if it does not exist.

* static void	 `write(File file, CharSequence data, Charset encoding, boolean append)`：Writes a CharSequence to a file creating the file if it does not exist.

* static void	 `write(File file, CharSequence data, String encoding)`：Writes a CharSequence to a file creating the file if it does not exist.

* static void	 `write(File file, CharSequence data, String encoding, boolean append)`：Writes a CharSequence to a file creating the file if it does not exist.

* static void	 `writeByteArrayToFile(File file, byte[] data)`：Writes a byte array to a file creating the file if it does not exist.

* static void	 `writeByteArrayToFile(File file, byte[] data, boolean append)`：Writes a byte array to a file creating the file if it does not exist.

* static void	 `writeByteArrayToFile(File file, byte[] data, int off, int len)`：Writes len bytes from the specified byte array starting at offset off to a file, creating the file if it does not exist.

* static void	 `writeByteArrayToFile(File file, byte[] data, int off, int len, boolean append)`：Writes len bytes from the specified byte array starting at offset off to a file, creating the file if it does not exist.

* static void	 `writeStringToFile(File file, String data, Charset encoding)`：Writes a String to a file creating the file if it does not exist.

* static void	 `writeStringToFile(File file, String data, Charset encoding, boolean append)`：Writes a String to a file creating the file if it does not exist.

* static void	 `writeStringToFile(File file, String data, String encoding)`：Writes a String to a file creating the file if it does not exist.

* static void	 `writeStringToFile(File file, String data, String encoding, boolean append)`：Writes a String to a file creating the file if it does not exist.

