# challenge Hunter-challenge-Write-up-


السلام عليكم ورحمة الله وبركاته


فكرة التحدي بالبداية إن عندي case مطلوب منّي كمحلل بإني أستخرج الموظف المشتبه به لما أجرأ أو أخل بأعمال غير قانونية فالموظف أدّعى بأنه ماكان عنده علم باللي يعمله فمطلوب مني كمحلل أحلل ماقام به المشتبه به .

رابط التحدي مرفق هنا  https://cyberdefenders.org/labs/32 ففي البداية راح نحلل سجل النظام عن طريق عدة أدوات راح أذكرها بالأسفل  

## الأدوات المطلوبة لحل التحدي:


1- [FTK Imager](https://accessdata.com/product-download/ftk-imager-version-4-3-1-1)

2- [Registry Explorer](https://ericzimmerman.github.io/#!index.md)

3- [RegRipper](https://github.com/keydet89/RegRipper3.0)

4- [Winprefetchview](https://winprefetchview.soft32.com/)

5- [Skyperious](https://suurjaak.github.io/Skyperious/downloads.html)

6- [Stellar Repair for Outlook](https://www.stellarinfo.com/outlook-pst-file-recovery.php?gclid=CjwKCAiAn5uOBhADEiwA_pZwcCqdLkBD5zgWXaLt_bFhA_FbvqkWutlFZLP2lFVlLfZaJ2iQXPQcjxoCUosQAvD_BwE)

7- [ShellBagsExplorer](https://ericzimmerman.github.io/#!index.md)

8- [JumpListExplorer](https://ericzimmerman.github.io/#!index.md)



## الحل كالتالي:


 بالبداية التحدي عبارة عن مجموعة أسئلة "30 سؤال" ولمعرفة حلها لابد من إجراء عدة عمليات تحليل فنبدأ الأن بأول سؤال 
 
 

## 1-	What is the computer name of the suspect machine?


سنبدأ من خلال تحليل ملفات سجل النظام أو ال WindowsRegistry  بالأجوبة على أول 8 أسئلة بإستخدام الأداتين Registry Explorer و Reg Ripper


بعد مايتم تنزيل التحدي على الجهاز وفك الضغط , ستكون الخطوات مبدئياَ بهذا الشكل من خلال FTK Imager سيتم تحليل الImage 


![Image file](https://github.com/MariamAlrashidi/-Hunter-challenge-Write-up-/blob/master/Pic/image%20file.jpg)



بعد كذا نحدد الملف المطلوب كما هو موضّح بالصورة


![Image file01](https://github.com/MariamAlrashidi/-Hunter-challenge-Write-up-/blob/master/Pic/image%20file01.jpg)




 من خلال تحليل Image بإستخدام FTK Imager سوف نجد ملفات Windows Registry ب المسارين (%Windir%\System32\Config) و (%UserProfile%\)
 
 
 
 ![Image file02](https://github.com/MariamAlrashidi/-Hunter-challenge-Write-up-/blob/master/Pic/image%20file02.jpg)
 
 
 
 
 
بالتعامل الأن مع برنامج Registry Explorer للإستكمال عملية تحليل التي تمت بشكل غير مصرّح له 
سنقوم بإختيار ملف الSystem

![System](https://github.com/MariamAlrashidi/-Hunter-challenge-Write-up-/blob/master/Pic/System.jpg)




 
 الأن نبدأ بحل الأسئلة فأول سؤال كان يطلب اسم الكمبيوتر لجهاز المشتبه به , لحل هذا السؤال راح يكون في مسار 
 
 (config\SYSTEM: ControlSet001\Control\ComputerName\ComputerName)
 
 
  



![Computer Name](https://github.com/MariamAlrashidi/-Hunter-challenge-Write-up-/blob/master/Pic/computer%20Name.jpg)



حل السؤال الأول سيكون : 4ORENSICS





## 2- What is the computer IP?

عشان نعرف ال Ip الخاص في المشتبه به في الغالب نتوجه لخانة السيرفر اللي تعامل معاها .. 
راح يكون المسار كالتالي :

(config\SYSTEM: ControlSet001\Services\Tcpip\Parameters\Interfaces\{8CB9FBF6-AE*****}

![IP](https://github.com/MariamAlrashidi/-Hunter-challenge-Write-up-/blob/master/Pic/ip.jpg)



حل السؤال الثاني سيكون كالتالي : 10.0.2.15



## 3- What was the DHCP LeaseObtainedTime?


السؤال الثالث فكرته إنه يتم حساب كم إستغرق المشتبه به بإن الip as live على DHCP في نفس صفحة السؤال السابق في هذا الجواب وحتى يتم حساب المدة يتم إستخدام هذا الموقع 
[epochconverter](https://www.epochconverter.com/)
فكرة هذا الموقع يحولها لقيمة مقروءة 


1- هنا قيمة قبل التحويل 
![DHCP](https://github.com/MariamAlrashidi/-Hunter-challenge-Write-up-/blob/master/Pic/DHCP.jpg)



2- هنا قيمتها كوقت إيجار المشتبه به للDHCP

![DHCP](https://github.com/MariamAlrashidi/-Hunter-challenge-Write-up-/blob/master/Pic/DHCP%20reader.jpg)







السؤال الرابع يتطلب مني معرفة الSID الذي إستعمله المشتبه به ولمعرفة ذلك سنتحقق من ملف الSAM  هذا الملف عبارة عن Security Account Manager ملف عبارة عن قاعدة بيانات يحتوي أو يخزّن كلمات مرور المستخدمين 

بالبداية نحدد ملف الSam بإستخدام برنامج الRegistry Explorer
![Sam File](https://github.com/MariamAlrashidi/-Hunter-challenge-Write-up-/blob/master/Pic/Sam%20file.jpg)


 نقدر نستخرجه من المسار التالي :

(config\SAM: SAM\Domains\Account\Aliases\Members\S-1-5-21-2489440558-2754304563-710705792)

![sid](https://github.com/MariamAlrashidi/-Hunter-challenge-Write-up-/blob/master/Pic/sid.jpg)

## 	4- What is the computer SID?
 S-1-5-21-2489440558-2754304563-710705792
 
 
 السؤال الخامس يتطلب مني معرفة إصدار نظام التشغيل الخاص بالمشتبه به ولمعرفة ذلك يكون بتحديد الSoftware الخاص به
 

![Software](https://github.com/MariamAlrashidi/-Hunter-challenge-Write-up-/blob/master/Pic/software.jpg)


ثم تحديد المسار التالي :
(config\SOFTWARE: Microsoft\Windows NT\CurrentVersion)

![8.1](https://github.com/MariamAlrashidi/-Hunter-challenge-Write-up-/blob/master/Pic/8.1.jpg)

## 5-  	What is the Operating System(OS) version?
8.1


السؤال السادس بحثنا عن طريق المسار التالي لإيجاد الtimezone
(config\SYSTEM: ControlSet001\Control\TimeZoneInformation)

![time zone](https://github.com/MariamAlrashidi/-Hunter-challenge-Write-up-/blob/master/Pic/tomezone.jpg)

بعذ كذا نسخنا الKey value الخاصة بالtimezone 
![time zone](https://github.com/MariamAlrashidi/-Hunter-challenge-Write-up-/blob/master/Pic/pts%20timezone.png)



## 6 - What was the computer timezone?
 UTC-07:00 
 
 
السؤال السابع طلب معرفة كم مرة المشتبه به قام بتسجيل دخول على الكمبيوتر , ولمعرفة هذا يتطلب مني تحليل ملف SAM
وعشان نحلل الملف نستخدم اداءة Reg Ripper
فكرة هذه الأداء ببساطة بإنها تستخرج لي المعلومات كقيم بحيث تحلل لي السجل أو الRegistry

الصورة هذه عملت في خانة ال Hive File ملف الSAM 
وخانة الReport file أنشاء ملف نصي بأسم Real log كما هو موضح بالصورة في الأسفل
![REAL log 01](https://github.com/MariamAlrashidi/-Hunter-challenge-Write-up-/blob/master/Pic/Real%20Log01.jpg)


بعد كذا عملت Rip! بحيث يستخرج لي معلومات الLog كما هو ظاهر في الصورة باللأسفل


![REAL log 02](https://github.com/MariamAlrashidi/-Hunter-challenge-Write-up-/blob/master/Pic/Real%20Log02.jpg)


في الملف الأخير ظهر لي جميع المعلومات كملف نصي كما أنشاءته بالسابق , ويظهر لي جواب السؤال السابع وهو عدد دخول المشتبه به وهو 3 مرات


![REAL log 03](https://github.com/MariamAlrashidi/-Hunter-challenge-Write-up-/blob/master/Pic/Real%20Log03.jpg)


## 7- How many times did this user log on to the computer?

3


بعد ماعرفنا كم مرة سجل دخول الأن نحاول نعرف آخر مرة تم تسجيل الدخول وهو ظاهر لنا بالملف النصي الذي إستخرجناه سابقاً

![REAL log 03](https://github.com/MariamAlrashidi/-Hunter-challenge-Write-up-/blob/master/Pic/Real%20Log03.jpg)


## 8- When was the last login time for the discovered account? Format: one-space between date and time

 2016-06-21 01:42:40 
 
 
 فكرة السؤال التاسع قائم على ال  “Network Scanner” كان على كمبوتر بيصير عليه هذا الScanner فمطلوب نعرف متى آخر مرة استخدمه المشتبه به 
 
 عشان نعرف وين صار فيه هذا ال “Network Scanner” راح نرجع للFTK Image نستخرج الملفات الموجودة في مجلد (windows/Prefetch) 
 ![Prefetch01](https://github.com/MariamAlrashidi/-Hunter-challenge-Write-up-/blob/master/Pic/Prefetch01.jpg)


ومن ثم إستخدمت اداءة Winprefetchview لتحليل أي ملف تم عمل الNetwork Scanner من خلاله 

>>>>>>>>>>>>>>>>>>>>>>>>>pic>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>


## 9 - There was a “Network Scanner” running on this computer, what was it? And when was the last time the suspect used it? Format: program.exe,YYYY-MM-DD HH:MM:SS UTC



<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<qu>>>>>>>>>>>>>>>>>>>>>>>>>>>>>
 
 

من خلال اداءة ال FTK Image إستخرجنا ملف الUsers لمعرفة كل الملفات تحت اسم المستخدم Hunter
![export users](https://github.com/MariamAlrashidi/-Hunter-challenge-Write-up-/blob/master/Pic/export%20users.jpg)

على سطح المكتب أو الDesktop حصلت ملف إسمه nmapscan.xml وهو عبارة عن نسخة أو ملف التقرير الناتج عن عملية الScanner
داخل الملف كان فيه تفاصيل عن وقت بداية ونهاية عملية الScan 

وقت البدء : 

 ![start](https://github.com/MariamAlrashidi/-Hunter-challenge-Write-up-/blob/master/Pic/starting.jpg)
 
 وقت الإنتهاء :
 
  ![end](https://github.com/MariamAlrashidi/-Hunter-challenge-Write-up-/blob/master/Pic/end.jpg)
  
 ## 10 - When did the port scan end? (Example: Sat Jan 23 hh:mm:ss 2016)
 Tue Jun 21 05:12:09 2016
  
نقدر من ملف الnmapscan.xml  نعرف عدد الports  المفتوحة 

  ![ports](https://github.com/MariamAlrashidi/-Hunter-challenge-Write-up-/blob/master/Pic/ports.jpg)
  
  
 ## 11 : How many ports were scanned?
 1000
 
 من نفس الملف راح نعرف عدد الports اللي تكون في حالة الopen
 
 ![open ports](https://github.com/MariamAlrashidi/-Hunter-challenge-Write-up-/blob/master/Pic/open%20ports.jpg)
 
 
 ## 12 : What ports were found "open"?(comma-separated, ascending)?
  22,80,9929,31337
  
  
  الأن مطلوب مننا نعرف نوع أو إصدار الNetwork Scannerاللي يشتغل على الكمبيوتر
  ولمعرفة الإصدار من نفس الملف السابق يتضح نوع الإصدار
  ![verison](https://github.com/MariamAlrashidi/-Hunter-challenge-Write-up-/blob/master/Pic/verison.jpg) 
   
## 13- What was the version of the network scanner running on this computer?

 7.12 
 
 
 مطلوب مننا إظهار الموظف اللي حاور مستخدم عبر الSkype 
 بالأول راح نستخرج ملف الSkype من خلال الFTK Image 
![skype](https://github.com/MariamAlrashidi/-Hunter-challenge-Write-up-/blob/master/Pic/skype01.jpg) 

بعد كذا نستخدم أداء Skyperious

راح نفتح ملفات ال Skype database من خلال اداء Skyperious

من خلال البحث في ملفات قاعدة البيانات في مجلد الSkype وجدنا المستخدم الآخر الذي تحاور معاها موظفنا 

![skype User](https://github.com/MariamAlrashidi/-Hunter-challenge-Write-up-/blob/master/Pic/skypeuser.jpg) 

## 14 - The employee engaged in a Skype conversation with someone. What is the skype username of the other party?

 linux-rul3z 
 
 الخطوة التالية بحثنا أيضاً بنفس الأداءة نقدر نوصل للمحادثة اللي تمت في Skype وبالتالي راح نوصل لجواب السؤال الآخر عن أي برنامج اتفقوا عليه
 
 ![teamv](https://github.com/MariamAlrashidi/-Hunter-challenge-Write-up-/blob/master/Pic/skypeuserteamv.jpg) 
 
 
 ## 15 - What is the name of the application both parties agreed to use to exfiltrate data and provide remote access for the external attacker in their Skype conversation?
 teamviewer
 
 
 
 من نفس الأداء نستخرج منه إيميل الموظف الذي تعاون مع المشتبه به 
 
  ![employ](https://github.com/MariamAlrashidi/-Hunter-challenge-Write-up-/blob/master/Pic/employe.jpg) 


## 16 - What is the Gmail email address of the suspect employee?

 ehptmsgs@gmail.com 
 
 
## 17 - It looks like the suspect user deleted an important diagram after his conversation with the external attacker. What is the file name of the deleted diagram?

عشان نحل هذا السؤال راح نتعامل مع أداء Stellar Repair for Outlook لتحليل ملفات البريد الإلكتروني 
لكن قبل التعامل معاها لابد من إستخراج الملفات بإستخدام الFTK Image راح استخرج مجلد الUsers كامل

  ![export backup](https://github.com/MariamAlrashidi/-Hunter-challenge-Write-up-/blob/master/Pic/export%20backup.jpg) 


الأن نحدد الملف اللي نحتاج نسترجعه من خلال اداء Stellar Repair for Outlook 
 
![backup](https://github.com/MariamAlrashidi/-Hunter-challenge-Write-up-/blob/master/Pic/backup.jpg)

راح نلقى الجواب في ملف الايميلات المحذوفة
 
![home network](https://github.com/MariamAlrashidi/-Hunter-challenge-Write-up-/blob/master/Pic/home-network-design.jpg)

جواب السؤال الماضي كالتالي 

## 17 - It looks like the suspect user deleted an important diagram after his conversation with the external attacker. What is the file name of the deleted diagram?

 home-network-design-networking-for-a-single-family-home-case-house-arkko-1433-x-792.jpg 
 
 

السؤال التالي 

## 18 - The user Documents' directory contained a PDF file discussing data exfiltration techniques. What is the name of the file?

بالرجوع للFTK Image يوجد لدينا ملف واضح لدينا بإمتداد PDF  وهذا هو الجواب 

![pdf](https://github.com/MariamAlrashidi/-Hunter-challenge-Write-up-/blob/master/Pic/PDF01.jpg)



فجواب السؤال مرة أخرى كالتالي :

## 18 - The user Documents' directory contained a PDF file discussing data exfiltration techniques. What is the name of the file?

Ryan_VanAntwerp_thesis.pdf

)))))))))))))))))))))))))))))))))))))))))))))))))))))))))))))))))))))))))))))))19(((((((((((((((((((((((((((((((((((((((((((((((((((((((((




السؤال التالي : طُلب معرفة الأرقام التسلسلية أو الserial numbers الخاصة بوحدتي التخزين الخاصة بالUSB

ولحل هذه المسألة نستخدم أداء ال Registry Explorerلقراءة ملف الUSB

من خلال المسار التالي :
(config\SYSTEM: ControlSet001\Enum\USB\ROOT_HUB20)

![usb](https://github.com/MariamAlrashidi/-Hunter-challenge-Write-up-/blob/master/Pic/usb.jpg)


## 20 - What are the serial numbers of the two identified USB storage?

 07B20C03C80830A9,AAI6UXDKZDV8E9OU
 
 
 <<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<21>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>
 
 
 
 
 ## 21 - How many prefetch files were discovered on the system?

عشان نعرف عدد الملفات الPrefetch اللي تم إكتشافها على النظام , راح نستخدم أداء winprefetchview ونرفع ملفات Prefetch ثم بعد ذلك نحذف الملفات ذات الحجم صفر فراح يتبقى لنا عدد 174 ملف
 
فالجواب على السؤال الماضي كالتالي :
 
  ## 22 - How many prefetch files were discovered on the system?
174
 
 
 
 
## 23- How many times was the file shredder application executed?
 
 
 
 ##24 - Using prefetch, determine when was the last time ZENMAP.EXE-56B17C4C.pf was executed?
 
 
 
 ## 25 - A JAR file for an offensive traffic manipulation tool was executed. What is the absolute path of the file?
 
 
 
في السؤال التالي الموظف المشتبه به حاول بسرقة البيانات عن طريق إرفاقها على الإيميل ولمعرفة ماتم إرفاقه راح أستعين بالإداء Stellar Repair for Outlook لتحليل ملفات البريد الإلكتروني
 
 فوجدنا بالإيميلات المُرسلة كالتالي :
 
 ![pic](https://github.com/MariamAlrashidi/-Hunter-challenge-Write-up-/blob/master/Pic/Pictures01.jpg)
 
 
 
## 26 - The suspect employee tried to exfiltrate data by sending it as an email attachment. What is the name of the suspected attachment?
 
  Pictures.7z 
 
 
 
 ## 27 - Shellbags shows that the employee created a folder to include all the data he will exfiltrate. What is the full path of that folder?
 
 
 
 
 >>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>
 
 
 ## 28 - The user deleted two JPG files from the system and moved them to $Recycle-Bin. What is the file name that has the resolution of 1920x1200?
 
 
 <<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<
 
 
 
 
 ## 29 - Provide the name of the directory where information about jump lists items (created automatically by the system) is stored?
   للجواب على هذا السؤال نعود ل FTK Image لمعرفة المجلدات التي بداخل مجلد الRecent
   راح تكون في المسار التالي 
  (%USERPROFILE%\AppData\Roaming\Microsoftg\Windows\Recent\AutomaticDestinations-ms)   
  ![Recent](https://github.com/MariamAlrashidi/-Hunter-challenge-Write-up-/blob/master/Pic/Recent.jpg)                                                                          
  فجواب السؤال السابق هو :  AutomaticDestinations-ms 
                                                                              
   
  ## 30 - Using JUMP LIST analysis, provide the full path of the application with the AppID of "aa28770954eaeaaa" used to bypass network security monitoring controls.
                                                                              
عشان نحلل ملفات الJump list نحتاج نستخرج هذه الملفات من الFTK Image من خلال المسار التالي نستخرج المعلومات اللي نحتاجها في عملة تحليل الملفات المطلوبة
 AppData\Roaming\Microsoftg\Windows\Recent\)
  راح نتعامل الأن مع اداء ال JumpListExplorer للتحليل .. راح نبحث عن ال AppID نفس ماهو مذكور بالسؤال فراح تكون الإجابة كالتالي :
                                                                              
                                                                              
