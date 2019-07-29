To get a comparison of the frequencies in two (or more) files, run

	./compare-frequencies <file-1> <file-2> <file-3> … <file-n>

Example:

	$ ./compare-frequencies 'data/general/黃帝內經 - Huangdi Neijing-邪氣藏府病形.txt' 'data/general/鹽鐵論 - Yan Tie Lun-西域.txt'
	Character, Rel. Freq. in data/黃帝內經 - Huangdi Neijing-邪氣藏府病形.txt, Rel. Freq. in data/鹽鐵論 - Yan Tie Lun-西域.txt
	卿, 0, 21482.277121374867
	不, 109463.2768361582, 139634.80128893664
	脹, 7062.146892655367, 0
	旌, 0, 10741.138560687432
	…

To view output in a spreadsheet, use the shell to redirect the output to a .csv file, then open it in your preferred program

Example:

	$ ./compare-frequencies 'data/黃帝內經 - Huangdi Neijing-邪氣藏府病形.txt' 'data/鹽鐵論 - Yan Tie Lun-西域.txt' > sheet.csv
	$ libreoffice --calc sheet.csv

Glob patterns can be used to compare sets of multiple files, such as complete chapters. However, be sure to surround with *single* quotes, as the glob patterns are interpretted by the `./compare-frequencies` script rather than the shell.

Example:
	
	$ ./compare-frequencies 'data/黃帝內經*' 'data/鹽鐵論*'

	Character, Rel. Freq. in data/黃帝內經*, Rel. Freq. in data/鹽鐵論*
	腋, 2729.02397260274, 165.5163281857755
	寒, 46660.95890410959, 5793.071486502144
	欺, 160.5308219178082, 1489.6469536719796
	裒, 0, 165.5163281857755
	…

To compare *every* file in the data set, run

	$ for e in data/*.txt; do echo $e; done | xargs -d "\n" ./compare-frequencies > sheet.csv

Frequency data for any file f is stored in f.json. To re-generate the files, using 4 seperate processes for speed, run:
	
	for e in data/*.txt; do echo $e; done | xargs -d "\n" -P 4 -n 1 cache

## Scripts in this Repository

<table>
<tr><td>Name</td><td>Function</td></tr>

<tr><td>`cache`</td><td>
Calls `frequency` on the given file `f` and outputs to `f.json`, with the characters in `stop.txt` excluded.
</td></tr>

<tr><td>`compare-frequencies`</td><td>
Takes a list of files and outputs a CSV comparing the occurences of the appearing characters.
</td></tr>

<tr><td>`frequency`</td><td>
Takes a file and outputs json containing the absolute and relative frequencies of each character in the file.
</td></tr>

<tr><td>`in-all`</td><td>
Takes a list of files and outputs the characters which appear in all of them, seperated by spaces. Also prints to stderr when the number of characters that have been seen in every file yet analyzed changes.
</td></tr>

<tr><td>`json-to-csv`</td><td>
Takes json produced by `frequency` through stdin into a CSV, printing to stdout.
</td></tr>

<tr><td>`make-csv`</td><td>
Converts json file `f` to csv and writes to `f.csv`.
</td></tr>

</table>
