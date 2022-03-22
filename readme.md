# license-header -- tool for adding license to source code files

license-header is a tool that can add/remove license information to source code files.  
The tool is written in Python 3.  

## Features

- Add license to source code files.
- Remove license from source code files.
- Update license in source code files, in case of the license has minor changes (such as changed the license date).
- Support change source files recursively.

## License

Apache License, Version 2.0  

## Source code

[https://github.com/wqking/license-header](https://github.com/wqking/license-header)

## Command line

```
python licenseheader.py ACTION [--help] [-h] --source SOURCE --license LICENSE [--before BEFORE] [--after AFTER] [--line-before LINE_BEFORE] [--line-after LINE_AFTER] [--exclude EXCLUDE]      
```

#### ACTION, required

The action can be `update` or `remove`.  
If the action is `update`, it will add the license to the source files if it's not there, or update the license if the license is already there.  
If the action is `remove`, it will remove the license from the source files.  

The tool matches license text with the source code using fuzzy matching algorithm. If the license is modified slightly, such as changing the license year, the tool can detect the license block in the source code correctly. But if the license is going to be changed a lot, you'd better remove the old license from the source code, then edit the license, then add the license back to the source code.  
Note: be sure to backup your source code files before using the tool.

#### --source SOURCE, required

SOURCE is the file pattern of the source files, the pattern can include wildcard `*`, and may include `**` to indicate recursive folders.  
There can be multiple `--source SOURCE`.  

#### --license LICENSE, required

LICENSE is the location of the license file. The tool reads the license file and add it in front of each source files.  
There can be only one `--license LICENSE`.  

#### --before BEFORE, optional

BEFORE is the text that will be added before the license block.  
If there are spaces, BEFORE should quoted with ".  
Any \n in the text will be replaced with line break.  

#### --after AFTER, optional

AFTER is the text that will be added after the license block.  
If there are spaces, AFTER should quoted with ".  
Any \n in the text will be replaced with line break.  

#### --line-before LINE_BEFORE, optional

LINE_BEFORE is the text that will be added before each line of the license.  
If there are spaces, AFTER should quoted with ".  
Any \n in the text will be replaced with line break.  

#### --line-after LINE_AFTER, optional

LINE_AFTER is the text that will be added after each line of the license.  
If there are spaces, AFTER should quoted with ".  
Any \n in the text will be replaced with line break.  

#### --exclude EXCLUDE, optional

Special the file names to be excluded from the source files.  
`EXCLUDE` can't contain any wildcard. The tool checks if any source file name or path contains `EXCLUDE`, then the tool skips that file.  
There can be multiple `--exclude EXCLUDE`.  


## Examples

#### Add license to Python source code

```
python licenseheader.py update --source /project/mylittleproject/src/**/*.py --license mylicense --line-before "# " --after ""
```
The `--after ""` is to add a blank line after the license block.

#### Add license to C++ source code

```
python licenseheader.py update --source /project/mylittleproject/include/**/*.h --source /project/mylittleproject/src/**/*.cpp --license mylicense --line-before "// " --after ""
```
