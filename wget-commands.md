# wget commands

### Download Only Certain File Types Using wget -r -A
You can use this under following situations:

  - Download all images from a website
  - Download all videos from a website
  - Download all PDF files from a website

`$ wget -r -A.pdf http://url-to-webpage-with-pdfs/`


### Download a Full Website Using wget –mirror
Following is the command line which you want to execute when you want to download a full website and made available for local viewing.

` $ wget --mirror -p --convert-links -P ./LOCAL-DIR WEBSITE-URL `

- -mirror : turn on options suitable for mirroring.
- -p : download all files that are necessary to properly display a given HTML page.
- -convert-links : after the download, convert the links in document for local viewing.
- -P ./LOCAL-DIR : save all the files and directories to the specified directory.

### Download Multiple Files / URLs Using Wget -i
First, store all the download files or URLs in a text file as:

<pre>$ cat > download-file-list.txt
URL1
URL2
URL3
URL4</pre>

Next, give the download-file-list.txt as argument to wget using -i option as shown below.
`$ wget -i download-file-list.txt`


- - - 

### Example 1

This downloaded the entire website for me:<br>

`wget --no-clobber --convert-links --random-wait -r -p -E -e robots=off -U mozilla http://site/path/`

- If the files are ignored for robots (e.g. search engines), you've to add also: `-e robots=off`

- - - 

### Example 2

I was trying to download zip files linked from Omeka's themes page - pretty similar task. This worked for me:<br>

`wget -A zip -r -l 1 -nd http://omeka.org/add-ons/themes/`

  - -A: only accept zip files
  - -r: recurse
  - -l 1: one level deep (ie, only files directly linked from this page)
  - -nd: don't create a directory structure, just download all the files into this directory.

All the answers with `-k, -K, -E` etc options probably haven't really understood the question, as those as for rewriting HTML pages to make a local structure, renaming .php files and so on. Not relevant.

To literally get all files except .html etc:<br>
`wget -R html,htm,php,asp,jsp,js,py,css -r -l 1 -nd http://yoursite.com`

- - - 

### Example 3

`wget -nd -r -l 2 -A jpg,jpeg,png,gif http://t.co`

  - -nd: no directories (save all files to the current directory; -P directory changes the target directory)
  - -r -l 2: recursive level 2
  - -A: accepted extensions

`wget -nd -H -p -A jpg,jpeg,png,gif -e robots=off example.tumblr.com/page/{1..2}`

  - -H: span hosts (wget doesn't download files from different domains or subdomains by default)
  - -p: page requisites (includes resources like images on each page)
  - -e robots=off: execute command robotos=off as if it was part of .wgetrc file. This turns off the robot exclusion which means you ignore robots.txt and the robot meta tags (you should know the implications this comes with, take care).

### Example 4
Sometimes you just have to be nice to the server ( flags: -e robots=off --user-agent=Mozilla )

`wget -r -A pdf -nd -e robots=off --user-agent=Mozilla site-url`