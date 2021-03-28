# reltodot — convert relations between files to the DOT language

**reltodot** (RELations TO DOT) is a utility that allows to create a graph in the DOT language from relations between files. A "relation" between at least two files is a character string that occurs in each of those files. A node represents a file; an edge between two files represent the [union](https://en.wikipedia.org/wiki/Union_(set_theory)) of all the relations between those files. Files with no relation to any other file are not included.

**Important — disclaimer:** The purpose of the utility that this project contains is to present working code rather than to be used in real life. It was not tested in any way warranting it to be run. If you run it, you do it under your own responsibility.

1. [Copyright note](#copyright-note)
2. [Dependencies](#dependencies)
3. [Usage](#usage)

## Copyright note

Note that this project has currently **no license**, as explained in [this GitHub guide on licensing projects](https://choosealicense.com/no-permission/).

For your convenience, I'm including below a quote from that site:

> When you make a creative work (which includes code), the work is under exclusive copyright by default. Unless you include a license that specifies otherwise, nobody else can copy, distribute, or modify your work without being at risk of take-downs, shake-downs, or litigation. Once the work has other contributors (each a copyright holder), “nobody” starts including you.

Also note that I can add a license in the future if it would be relevant to the needs of this project.

## Dependencies

The platform/operating system to run the utility on must fulfill all of the following conditions:

- the operating system is Linux;
- the shell is GNU bash in version 5.0.17(1), and its path is `/bin/bash`;
- all of the following utilities are available in `$PATH` (under the names given):
    - GNU grep in version 3.4
    - GNU sed in version 4.8
    - GNU join, GNU coreutils in version 8.32
    - GNU cut, GNU coreutils in version 8.32
    - GNU sort, GNU coreutils in version 8.32
    - GNU uniq, GNU coreutils in version 8.32
    - GNU paste, GNU coreutils in version 8.32
    - GNU head, GNU coreutils in version 8.32

In case any of the above conditions is not fulfilled, it is unknown how the utility will behave; it may just not work, or it may cause damage to the platform, and/or the operating system, and/or any files.

## Usage

**Important:** Before using the utility, one has to ensure that the platform they are to run it on fulfills the conditions listed in the section [Dependencies](#dependencies) of this README.

This utility is a command line utility. It writes its normal output to stdout, errors to stderr, and takes some of its input from stdin.

To create a graph, one invokes it as follows:

```
<bash command> reltodot '<regular expression>'
```

where:

- `<bash command>` is a command to run Bash (usually just `bash`); it is to be provided to stdin a list of newline-separated file paths; the list may be empty; a path must fulfill all of the following conditions:
    - it is a path to a regular file,
    - it does not contain neither newlines, tabs, backslashes nor double quotes;
- `<regular expression>` is a [PCRE](https://en.wikipedia.org/wiki/Perl_Compatible_Regular_Expressions) regular expression that represents a group of character strings representing the relations between the files; it must not be empty.

## Examples

Assuming the commands `find` and `bash` are available, the commmand `find` represents the find utility from the GNU findutils and the command `bash` represents GNU bash, the following invokation creates a graph from all the regular files in the current working directory that all contain either the character string 'foo' or the character string 'bar':

```
find . -type f | bash reltodot 'foo|bar'
```
