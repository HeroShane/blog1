---
layout: post
title: 总结整理：Apache FilenameUtils
categories:
    - java
tags:
    - java
    - FilenameUtils
excerpt: Apache FilenameUtils
---


* static String	 `concat(String basePath, String fullFilenameToAdd)`：Concatenates a filename to a base path using normal command line style rules.

* static boolean	 `directoryContains(String canonicalParent, String canonicalChild)`：Determines whether the parent directory contains the child element (a file or directory).

* static boolean	 `equals(String filename1, String filename2)`：Checks whether two filenames are equal exactly.

* static boolean	 `equals(String filename1, String filename2, boolean normalized, IOCase caseSensitivity)`：Checks whether two filenames are equal, optionally normalizing and providing control over the case-sensitivity.

* static boolean	 `equalsNormalized(String filename1, String filename2)`：Checks whether two filenames are equal after both have been normalized.

* static boolean	 `equalsNormalizedOnSystem(String filename1, String filename2)`：Checks whether two filenames are equal after both have been normalized and using the case rules of the system.

* static boolean	 `equalsOnSystem(String filename1, String filename2)`：Checks whether two filenames are equal using the case rules of the system.

* static String	 `getBaseName(String filename)`：Gets the base name, minus the full path and extension, from a full filename.

* static String	 `getExtension(String filename)`：Gets the extension of a filename.

* static String	 `getFullPath(String filename)`：Gets the full path from a full filename, which is the prefix + path.

* static String	 `getFullPathNoEndSeparator(String filename)`：Gets the full path from a full filename, which is the prefix + path, and also excluding the final directory separator.

* static String	 `getName(String filename)`：Gets the name minus the path from a full filename.

* static String	 `getPath(String filename)`：Gets the path from a full filename, which excludes the prefix.

* static String	 `getPathNoEndSeparator(String filename)`：Gets the path from a full filename, which excludes the prefix, and also excluding the final directory separator.

* static String	 `getPrefix(String filename)`：Gets the prefix from a full filename, such as C:/ or ~/.

* static int	 `getPrefixLength(String filename)`：Returns the length of the filename prefix, such as C:/ or ~/.

* static int	 `indexOfExtension(String filename)`：Returns the index of the last extension separator character, which is a dot.

* static boolean	 `isExtension(String filename, Collection<String> extensions)`：Checks whether the extension of the filename is one of those specified.

* static boolean	 `isExtension(String filename, String extension)`：Checks whether the extension of the filename is that specified.

* static boolean	 `isExtension(String filename, String[] extensions)`：Checks whether the extension of the filename is one of those specified.

* static String	 `removeExtension(String filename)`：Removes the extension from a filename.

* static String	 `separatorsToSystem(String path)`：Converts all separators to the system separator.

* static String	 `separatorsToUnix(String path)`：Converts all separators to the Unix separator of forward slash.

* static String	 `separatorsToWindows(String path)`：Converts all separators to the Windows separator of backslash.
