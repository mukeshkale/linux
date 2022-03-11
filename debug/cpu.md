##### Check No of CPU(s)/processors you system has:
`grep -c ^processor /proc/cpuinfo`

``!---------------!		
!	12	!
!---------------!``
##### Chek CPU Multi-threading/Hyper-threading capability/support if you see below: 
dmidecode -t processor | grep HTT

!-------------------------------!
!	HTT (Multi-threading)	!
!	HTT (Multi-threading)	!
!-------------------------------!

###In Case of HyperThreading disabled : 
lscpu | grep -i -E  "^CPU\(s\):|core|socket"

!---------------------------------------!
!	CPU(s):                12	!
!	Thread(s) per core:    1	!
!	Core(s) per socket:    6	!
!	Socket(s):             2	!
!---------------------------------------!	

###In Case of HyperThreading enabled : 
lscpu | grep -i -E  "^CPU\(s\):|core|socket"

!---------------------------------------!
!	CPU(s):                4	!
!	Thread(s) per core:    2	!	
!	Core(s) per socket:    2	!
!	Socket(s):             1	!
!---------------------------------------!

###In Case of HyperThreading disabled : 
grep -E "cpu cores|siblings|physical id" /proc/cpuinfo | xargs -n 11 echo |sort |uniq 

!-------------------------------------------------------!
!	physical id : 0 siblings : 6 cpu cores : 6	!
!	physical id : 1 siblings : 6 cpu cores : 6	!
!-------------------------------------------------------!

###In Case of HyperThreading enabled : 
##If siblings are double than cores that means Multi-threading/Hyper threading enabled. 
grep -E "cpu cores|siblings|physical id" /proc/cpuinfo | xargs -n 11 echo |sort |uniq 

!-------------------------------------------------------!
!	physical id : 0 siblings : 4 cpu cores : 2 	!
!-------------------------------------------------------!

##In the case above, siblings is 2 times than cores, thus, the host is HT enabled.


