### Converting video to gif with ffmpeg
```bash
ffmpeg -i in.mov -pix_fmt rgb8 -r 10 output.gif
```

### Repeating some command until it will work
```bash
until some command ; do sleep 5 ; done
until git push ; do sleep 5 ; done
```

### Sourcing (exporting) env variables
```bash
set -a
source env_file.env
set +a
```

### Replacing text in the file:
```bash
sed -i "s/what-we-searching/what-we-replacing/g" file.txt
sed -i'.bak' "s/what-we-searching/what-we-replacing/g" file.txt
```
`-i'.back'` is for backup file, (MacOS sed implementation)

### Replacing text in all files recursively
```bash
find . -type f -exec sed -i 's/foo/bar/g' {} +
```

#### Find all python files, that contains `module_name` and rename them to `new_module_name`:
```
find . -type f -name '*.py' ! -name '*__pycache__*' ! -path '*__pycache__*' -exec sed -i'.bak' "s/app_name/new_module_name/g" {} +
git clean -n # show files to be cleaned
git clean -f  # clean non-tracked files (as sed will create .bak files)
```

### Strange symbols when clicking in terminal
```bash
reset
```

### Extract from tar
```bash
tar -xvzf archive.tar.gz -C directory
```

### Compress with tar
```bash
tar -czf name_of_archive_file.tar.gz name_of_directory_to_tar
```

### Compress pdf with ghostscript

#### Install it with brew:
```bash
arch -arm64 brew install ghostscript
```

#### Run script
```
gs \
-sDEVICE=pdfwrite \
-dCompatibilityLevel=1.4 \
-dPDFSETTINGS=/printer \
-dBATCH \
-dNOPAUSE \
-dQUIET \
-sProcessColorModel=DeviceGray \
-sColorConversionStrategy=Gray \
-dOverrideICC \
-sOutputFile=output.pdf \
input.pdf
```

#### Or create bash command:
```
vi ~/.zshrc
...
# Usage: compresspdf [input file] [output file] [screen*|ebook|printer|prepress]
compresspdf() {
    gs -sDEVICE=pdfwrite -dNOPAUSE -dQUIET -dBATCH -dPDFSETTINGS=/${3:-"screen"} \
        -dColorImageResolution=150 -dCompatibilityLevel=1.4 -sOutputFile="$2" "$1"
}
```

```bash
compresspdf ~/Downloads/Mokhova_Kristina_zagran_new.pdf ~/Downloads/Small_new_k_zagran.pdf printer
```

### Measure script execution time
```bash
start=`date +%s` && do_your_stuff && end=`date +%s`; echo Execution time was: `expr $end - $start`s
```

### Copy all files except some file/dir
```bash
rsync -aP --exclude=file_exclude.md --exclude=.git/ ../old_folder/* .
```

### Search through all files and folders in files content
```bash
grep -ir "text_to_search" .
```

#### Reversed grep (invert | reversing)
```bash
grep -v "text" somefile.txt
```

### Get last several characters
```bash
echo ${foo: -3} # get last 3 characters
echo ${foo##*.} # get last characters to "." (dot)

```

### Grep infromation from files recursibely, get filename from that and print only unique:
```bash
grep -irn "retention" . | awk -F: '{print $1}' | sort -u
```

### Grep subdirectories and show 1 line before (parent)
```
ls */ | grep --color -i -B 1 "pattern"
```
- `-B {number}` - show lines before match
- `-A {number}` - show lines after match

### Working with JQ
- https://www.baeldung.com/linux/jq-command-json

### Recursevly go to subdirectories and checking git
```
current_dir=$(pwd); for i in $(ls -1); (cd $(pwd)/$i/; echo "$i $( git rev-parse --abbrev-ref HEAD)"; git checkout mainline);
```
