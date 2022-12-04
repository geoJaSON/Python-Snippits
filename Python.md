
**Read a JSON from URL**

    with urllib.request.urlopen(<url>) as url:  
	    data = json.loads(url.read().decode())

**Post**

    import requests,json  
    x = requests.post(<url>)
    res = json.loads(x.text)
**Fetch file from URL**

    x=requests.get(<url>).content

**Read URL**

    with request.urlopen(r<url>) as response:  
	    source = response.read()  
    data = json.loads(source)


 ## Files and Folders
**Walk Directory**

    for root, dirs, files in os.walk("D:\photos", topdown=False):

**Remove File**

    os.remove(f)

**Create File Path**

    os.path.join(<part 1>,<part 2>)

**List Files**

    os.listdir()

**Get Working Directory**

    os.getcwd()

**Change Working Directory**

    os.chdir(<path>)

**Make Directory**

    os.mkdir(<path>)

## Misc
**Show Exception Details**

    except Exception as e:  
	    exc_type, exc_obj, exc_tb = sys.exc_info()  
	    print(exc_type, e, "line " + str(exc_tb.tb_lineno))

**Print Last Declared Variable**

    _

**Loop through Dictionary**

    for key, value in <dict>.items():

**List Comprehension**

    newlist = [ expression for item in list if conditional ]

**Lambda**

    (lambda x: x + 1)(2) = lambda 2: 2 + 1
    ex) add_one = lambda x: x + 1
    add_one(2)


**Dynamic Variable**

    locals()[<variable>]

**Iterate Printing**

    print("29", "01", "2022", sep="/") # 29/01/2022

**Merge Dictionary**

    merged = {**dictionary_one, **dictionary_two}

**Test if String Starts With**

    print(my_string.startswith("b"))

**If Any or All Conditions**

    my_conditions = [math_points > 50, biology_points > 50,  physics_points > 50, history_points > 50]  
    if all(my_conditions):  
    	print("Congratulations! You have passed all of the exams.")
    if any(my_conditions):  
    	print("Congratulations! You have passed all of the exams.")

**Enumerate**

    for index, element in enumerate(listOne):  
	    print("Index [", index,"]", "Value", element)

**Create Dictionary from Two Lists**

    itemDictionary = dict(zip([list1], [list2]))  
## Time and Dates
**Get time as string**

    timestr = datetime.now().strftime("%Y%m%d%H%M%S")
**Dates**

    d0 = date(2020, 12, 14)
    tdate = date.today()
    delta = tdate - d0
    daysdelta = delta.days

**Yesterday**

    yesterday = datetime.now() + timedelta(-1)

**Stringify Date**

    datetime.strftime(<date object>, '%Y-%m-%d')

**Show Total Processing Time**

    import time  
    startTime = time.time()  
    ...  
    endTime = time.time()  
    totalTime = endTime - startTime  
    print("Total time required to execute code is= ", totalTime)
**Time Formats**
|    |                                                |                          |
| -- | ----------------------------------------------------------- | ------------------------ |
| %a | Weekday, short version                                      | Wed                      |
| %A | Weekday, full version                                       | Wednesday                |
| %w | Weekday as a number 0-6, 0 is Sunday                        | 3                        |
| %d | Day of month 01-31                                          | 31                       |
| %b | Month name, short version                                   | Dec                      |
| %B | Month name, full version                                    | December                 |
| %m | Month as a number 01-12                                     | 12                       |
| %y | Year, short version, without century                        | 18                       |
| %Y | Year, full version                                          | 2018                     |
| %H | Hour 00-23                                                  | 17                       |
| %I | Hour 00-12                                                  | 5                        |
| %p | AM/PM                                                       | PM                       |
| %M | Minute 00-59                                                | 41                       |
| %S | Second 00-59                                                | 8                        |
| %f | Microsecond 000000-999999                                   | 548513                   |
| %z | UTC offset                                                  | 100                      |
| %Z | Timezone                                                    | CST                      |
| %j | Day number of year 001-366                                  | 365                      |
| %U | Week number of year, Sunday as the first day of week, 00-53 | 52                       |
| %W | Week number of year, Monday as the first day of week, 00-53 | 52                       |
| %c | Local version of date and time                              | Mon Dec 31 17:41:00 2018 |
| %C | Century                                                     | 20                       |
| %x | Local version of date                                       | 12/31/18                 |
| %X | Local version of time                                       | 17:41:00                 |
