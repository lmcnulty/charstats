To get a comparison of the frequencies in two files, run

	./compare-frequencies <file-1> <file-1>

Example:

	$ ./compare-frequencies 'data/黃帝內經 - Huangdi Neijing-邪氣藏府病形.txt' 'data/鹽鐵論 - Yan Tie Lun-西域.txt'
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


