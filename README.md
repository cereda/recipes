# Recipes

This repository holds a lot of stuff I use, for good or for bad. Use it at your own risk (if you dare, of course). `:)`

*Basename and extension of a file:*

```bash
filename=$(basename "$fullfile")
extension="${filename##*.}"
filename="${filename%.*}"
```

*A couple of settings for Vim:*

```
syntax on
filetype plugin indent on
set nocompatible
set nobackup
set nowritebackup
set noswapfile
set encoding=utf8
set expandtab
set shiftwidth=4
set tabstop=4
set smarttab
set ruler
set number
```

*If you want Vim to understand Windows mappings:*

```
source $VIMRUNTIME/mswin.vim
behave mswin
```

*Enable Pathogen in Vim:*

```
call pathogen#infect()
```

*Remove metadata from a multimedia file:*

```
ffmpeg -i in.mov -map_metadata -1 -c:v copy -c:a copy out.mov
```

*Convert an audio file to OGA:*

```
ffmpeg -i in.mp3 -f ogg -vn -sn -acodec libvorbis -ab 192k out.oga
```

*TeX Live path script for Fedora:*

```bash
#!/bin/bash
pathmunge () {
    if ! echo $PATH | /bin/egrep -q "(^|:)$1($|:)" ; then
        if [ "$2" = "after" ] ; then
            PATH=$PATH:$1
        else
            PATH=$1:$PATH
        fi
    fi
}
pathmunge /opt/texbin
unset pathmunge
```

*Set a doclet for Maven:*

```xml
<plugin>
    <groupId>org.apache.maven.plugins</groupId>
    <artifactId>maven-javadoc-plugin</artifactId>
    <version>2.9.1</version>
    <configuration>
        <doclet>full.class.path</doclet>
        <docletPath>/full/class/to/file.jar</docletPath>
        <additionalparam>additional parameters</additionalparam>
        <useStandardDocletOptions>false</useStandardDocletOptions>
    </configuration>
</plugin>
```

*My personal script on converting video files to WEBM:*

```bash
#!/bin/bash
 
function usage {
    echo "No arguments provided. The script will end."
    exit 1
}
 
if [ -z "$1" ]
then
    usage
fi
 
filename=$(basename "$1")
extension="${filename##*.}"
filename="${filename%.*}"
 
echo "Converting file to WEBM..."
ffmpeg -i "$filename.$extension" -codec:v libvpx -quality good -cpu-used 0 -b:v 500k -qmin 10 -qmax 42 -maxrate 500k -bufsize 1000k -threads 4 -vf scale=-1:480 -codec:a libvorbis -b:a 128k "$filename.webm"
```

*Collecting the command output in Commons Exec:*

```java
import java.util.LinkedList;
import java.util.List;
import org.apache.commons.exec.LogOutputStream;
 
public class CollectingLogOutputStream extends LogOutputStream {

    private final List lines = new LinkedList();

    @Override protected void processLine(String line, int level) {
        lines.add(line);
    }

    public List getLines() {
        return lines;
    }

}
```

*Singleton template for Netbeans:*

```java
/**
* Singleton reference of ${TYPE default="Object"}.
*/
private static ${TYPE default="Object"} ${OBJ newVarName default="selfRef"};
/**
* Constructs singleton instance of ${TYPE default="Object"}.
*/
private ${TYPE}(){
    ${OBJ selfRef default="selfRef"} = this;
}
 
${cursor}
/**
* Provides reference to singleton object of ${TYPE default="Object"}.
* @return Singleton instance of ${TYPE default="Object"}.
*/
public static final ${TYPE default="Object"} getInstance(){
    if(${OBJ selfRef default="selfRef"}==null)
        ${OBJ selfRef default="selfRef"} = new ${TYPE}();
    return ${OBJ selfRef default="selfRef"};
}
```

*Get the order of pages for a booklet:*

```python
pages = int(input("How many pages? "))
if pages % 4 != 0:
    pages = pages + (4 - (pages % 4))
    print("Page number is not a multiple of four. Fixing it to " + str(pages) + ".")
 
counterDown = pages
counterUp = 1
result = []
isEven = False
 
while (counterDown > counterUp):
 
    if isEven:
        result.append(counterUp)
        result.append(counterDown)
        isEven = False
    else:
        result.append(counterDown)
        result.append(counterUp)
        isEven = True

    counterDown = counterDown - 1
    counterUp = counterUp + 1
 
print(result)
```

*Look for classes inside a JAR file:*

```bash
grep -Hls ClassName file.jar
```

*Extract audio from video:*

```bash
ffmpeg -i video.mp4 -ab 160k -ac 2 -ar 44100 -vn audio.mp3
```

To be continued.
