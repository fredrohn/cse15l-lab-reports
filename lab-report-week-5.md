# Lab Report Week 5

In week 4, we learned about bash scripts and useful commands. Below, I will explore the grep command and useful options. 

The basic format to use a grep command is as follows: 

```
$ grep <string> <file>
```

Options can be added on at it's tail. 

## The -l option

To use this option, type the following command: 
```
$ grep <string> <file-1> <file-2>...<file-n> -l
```
The `-l` command lists which input files contain the string we are searching for. This is useful because because if we don't know how big the output is going to be, it will let us find out which files have what we want without cluttering our terminal.

Here are three examples of me using it on the `./technical` directories/files.

### Example 1
```
fred@nurbaitis-mbp-2 technical % grep "United 175 was hijacked" 911report/*.txt -l
911report/chapter-1.txt
```
Here, I'm in the `./technical` directory. The output shows which txt files within `/911report`, in this case only `/chapter-1.txt`, contain the string that I am searching for. 

### Example 2

```
fred@nurbaitis-mbp-2 technical % grep "175" 911report/*.txt -l 
911report/chapter-1.txt
911report/chapter-13.2.txt
911report/chapter-13.3.txt
911report/chapter-13.4.txt
911report/chapter-13.5.txt
911report/chapter-7.txt
911report/chapter-9.txt
```
This example is similar to Example 1, but searches for a string that occurs in multiple files. It prints out all the files that have the string. 

### Example 3

If you search for a string that doesn't exist, there is not output. 

```
fred@nurbaitis-mbp-2 technical % grep "United 175 was hijacked by bob" 911report/*.txt -l
fred@nurbaitis-mbp-2 technical % 
```

This example is similar to example 1, but searches for a string that doens't occur at all. 

## The -n option

To use this option, type the following command: 
```
$ grep <string> <file-1> <file-2>...<file-n> -n
```
On top of printing the lines of the file that contain the string that we are searching for, the `-n` option shows the file that it's in and the line number where the string occurs. This is useful if the file is really large because the user now has a way to locate it without searching through the whole file. 

### Example 1
```
fred@nurbaitis-mbp-2 technical % grep "United 175 was hijacked" 911report/*.txt -n
911report/chapter-1.txt:158:    United 175 was hijacked between 8:42 and 8:46, and awareness of that hijacking began to spread after 8:51. American 77 was hijacked between 8:51 and 8:54. By 9:00, FAA and airline officials began to comprehend that attackers were going after multiple aircraft. American Airlines' nationwide ground stop between 9:05 and 9:10 was followed by a United Airlines ground stop. FAA controllers at Boston Center, which had tracked the first two hijackings, requested at 9:07 that Herndon Command Center "get messages to airborne aircraft to increase security for the cockpit." There is no evidence that Herndon took such action. Boston Center immediately began speculating about other aircraft that might be in danger, leading them to worry about a transcontinental flight-Delta 1989-that in fact was not hijacked. At 9:19, the FAA's New England regional office called Herndon and asked that Cleveland Center advise Delta 1989 to use extra cockpit security.
```
Here, from the `./techincal` directory, the string is being searched within all `.txt` files inside `/911report`. It finds the occurance at line 158 of `/chapter-1.txt`, which is printed before the actual line. 

### Example 2

If you search for a file that doesn't exist, there is no output. 

```
fred@nurbaitis-mbp-2 technical % grep "United 175 was hijacked by bob" 911report/*.txt -n
fred@nurbaitis-mbp-2 technical %
```

This example is similar to example 1, but searches for a string that doesn't exist. There is no output. 

### Example 3

Because it prints the entire line, similar to the original grep command, outputs can be very large. 
```
fred@nurbaitis-mbp-2 Media % grep "farm" *.txt -n
Avoids_Budget_Cut.txt:83:farmers and people with disabilities. Legal Services provides
Farm_workers.txt:8:The farm workers said they knew they had breathed poison moments
Farm_workers.txt:11:Most of the 20 migrant farm workers, in an adjacent lettuce
Farm_workers.txt:16:The farm workers in the western Colorado community said they
Farm_workers.txt:21:the Rocky Mountain region, says such migrant workers at farms
Farm_workers.txt:24:The company that hired the workers for the Olathe farm and the
Farm_workers.txt:25:farmer whose land they were working have denied any role in making
Farm_workers.txt:33:Another farm worker, 22-year-old Marcelina Lopez, was five
Farm_workers.txt:44:Ariz., farm-labor contractor that employs the crew - said company
Farm_workers.txt:50:'I think this is a crock,' said Humphrey, a vegetable farmer for
Farm_workers.txt:55:cases around the state. She and the other farm workers said they
Farm_workers.txt:60:Legal Services, which reports that migrant workers at farms
Farm_workers.txt:63:The exposure comes from chemical residue on plants in farm
Farm_workers.txt:66:Legal Services conducted interviews with 88 farm workers in some
Farm_workers.txt:73:interviews at farm-labor housing in those regions.
Farm_workers.txt:77:'It's striking that so many farm workers report experiencing
Farm_workers.txt:82:Bureau, said growers on the state's 20,000 farms consider pesticide
Farm_workers.txt:87:properly. I think farmers across the United States realize that,'
Farm_workers.txt:89:Yet the Legal Services report faults growers, farm-labor
Farm_workers.txt:96:The laws require that farm workers be prevented from entering
Farm_workers.txt:105:farms, and 20 failed to fully comply with federal laws meant to
Farm_workers.txt:106:protect farm workers from pesticides, said Tim Osag, an enforcement
Farm_workers.txt:107:coordinator. Those farms got warning letters and will be inspected
Farm_workers.txt:112:an EPA enforcement officer who conducted most of the farm
Farm_workers.txt:117:Migrant farm workers - 16,000 to 40,000 in Colorado, according
Farm_workers.txt:119:billion agriculture industry. They travel from farm to farm,
Farm_workers.txt:124:Many migrant farm workers are reluctant to report pesticide
Farm_workers.txt:135:leading health concern among migrant farm workers. Coloring books
Farm_workers.txt:136:distributed to the children of farm workers in Weld County warn
Farm_workers.txt:140:underscore the dangers of pesticides to farm workers and their
Farm_workers.txt:145:pesticides on farmworkers. The report, 'Fields of Poison,' found
Farm_workers.txt:146:that California farmworkers face greater risk of pesticide
Farm_workers.txt:152:effects of pesticides on farm workers.
Farm_workers.txt:155:migrant farm workers in California, most of them Hispanic, have a
Farm_workers.txt:163:Researchers compared farm worker data from United Farm Workers
GreensburgDailyNews.txt:11:Growing up on a farm near St. Paul, L. Mark Bailey didn't dream
Legal-aid_chief.txt:17:German bought into a coffee farm in Costa Rica and later adopted
Legal-aid_chief.txt:97:boots. A friend persuaded him to see a coffee farm in Costa Rica,
Legal-aid_chief.txt:99:German and two partners still own the 60-acre farm. He and his
Legal-aid_chief.txt:102:coffee the farm produces each year.
Marylands_Legal_Aid.txt:74:elderly, migrant farm workers, and neglected and abused children.
Nonprofit_Buys.txt:23:services from farm worker-related aid to basic assistance last year
Nonprofit_Buys.txt:28:farm labor and has represented large groups of workers. The basic
Nonprofit_Buys.txt:42:former justice came from a farm worker family that toiled in fields
Nonprofit_Buys.txt:50:farm workers and other poor people statewide for 35 years. Its
Nonprofit_Buys.txt:51:Oxnard office has provided services exclusively to farm workers for
Nonprofit_Buys.txt:55:farm workers.
Too_Crucial_to_Take_Cut.txt:58:children who are maltreated, migrant and seasonal farm workers who
Unusual_Woodburn.txt:10:For decades, Oregon farmworkers have raised these issues in
Unusual_Woodburn.txt:16:indigenous farmworkers from Mexico and Central America can find
Unusual_Woodburn.txt:20:the language and culture of the Spanish-speaking farmworker
Unusual_Woodburn.txt:29:She says indigenous farmworkers, driven north by economic hardship,
Unusual_Woodburn.txt:105:farmworkers. The project is funded by a two-year, $80,000
Unusual_Woodburn.txt:117:Nargess Shadbeh, director of the Oregon Law Center's farmworker
families_saved.txt:26:farm workers. In October 2000 Jennings gave the park residents
water_fees.txt:18:Alpaugh Irrigation District, which supplies water to farmers in the
water_fees.txt:42:Tuesday when a screaming and crying farmworker arrived.
water_fees.txt:43:The farmworker thought the water was getting turned off today,
```

Here, I am in the `/Media` directory searching for a string that occurs several times in multiple files. It is printing each line that has the string I am looking for along with the file and line number. 

## The -c option

To use this option, type the following command: 
```
$ grep <string> <file-1> <file-2>...<file-n> -c
```

The `-c` prints the number of lines in a file that contain the string being searched. This option is useful once you know what files contain the string you are looking for, but don't know at what volume. By knowing how much is in where before you print out the lines, you can avoid enormous outputs. 

### Example 1

```
fred@nurbaitis-mbp-2 technical % grep "United 175 was hijacked" 911report/*.txt -c
911report/chapter-1.txt:1
911report/chapter-10.txt:0
911report/chapter-11.txt:0
911report/chapter-12.txt:0
911report/chapter-13.1.txt:0
911report/chapter-13.2.txt:0
911report/chapter-13.3.txt:0
911report/chapter-13.4.txt:0
911report/chapter-13.5.txt:0
911report/chapter-2.txt:0
911report/chapter-3.txt:0
911report/chapter-5.txt:0
911report/chapter-6.txt:0
911report/chapter-7.txt:0
911report/chapter-8.txt:0
911report/chapter-9.txt:0
911report/preface.txt:0
```
Here, I'm in the `./technical` directory, searching for files within `/911report` that have the string I'm searching for. In all these files, the string only occurs once within `/chapter-1.txt`. 

### Example 2

If we only search in one file, it doesn't include the name of the file, only the amount of occurances. 

```
fred@nurbaitis-mbp-2 911report % grep "United 175 was hijacked" chapter-1.txt -c  
1
```
Here, I'm in the `/911report` directory, and I am only searching in the `/chapter-1.txt` file. The output is only a number. 

### Example 3

```
fred@nurbaitis-mbp-2 technical % grep "175" 911report/*.txt -c 
911report/chapter-1.txt:28
911report/chapter-10.txt:0
911report/chapter-11.txt:0
911report/chapter-12.txt:0
911report/chapter-13.1.txt:0
911report/chapter-13.2.txt:40
911report/chapter-13.3.txt:1
911report/chapter-13.4.txt:4
911report/chapter-13.5.txt:6
911report/chapter-2.txt:0
911report/chapter-3.txt:0
911report/chapter-5.txt:0
911report/chapter-6.txt:0
911report/chapter-7.txt:1
911report/chapter-8.txt:0
911report/chapter-9.txt:3
911report/preface.txt:0
```

Example 3 is similar to example 1, except that it searches for a string that occurs multiple times and in multiple files. 
